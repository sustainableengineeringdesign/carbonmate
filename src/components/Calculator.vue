<script setup>
import ImportIcon from "vue-material-design-icons/Import.vue"
import ExportIcon from "vue-material-design-icons/Export.vue"
import ReloadIcon from "vue-material-design-icons/Reload.vue"
import PlusIcon from "vue-material-design-icons/Plus.vue"
import MinusIcon from "vue-material-design-icons/Minus.vue"

import { reactive, computed, useTemplateRef } from 'vue'
import MaterialData from '../assets/materials.json'
import Papa from 'papaparse'

var defaultmaterial = Object.keys(MaterialData)[0]
var defaulttype = Object.keys(MaterialData[defaultmaterial])[0]
const boq = reactive([
  { material: defaultmaterial, type: defaulttype, mass: 12 }
])

function addnewtoboq() {
  boq.push({ material: defaultmaterial, type: defaulttype, mass: 0 })
}

function deletefromboq(idx) {
  boq.splice(idx,1)
}

function resetboq() {
  boq.splice(0, Infinity, { material: defaultmaterial, type: defaulttype, mass: 0 })
}

const totalemission = computed(() => boq.reduce(
  (acc,mat) => {
    let curr = MaterialData[mat.material][mat.type]["embodied carbon factor"] * mat.mass
    return acc + curr
  },
  0
))

const colorseq = ["red", "orange", "amber", "lime", "green"]
const commentseq = ["Very Poor", "Poor", "Average", "Good", "Excellent"]
const totalemissionidx = computed(() => { 
  if (totalemission.value < 100) { return 5 }
  else if (totalemission.value < 300) { return 4 }
  else if (totalemission.value < 600) { return 3 }
  else if (totalemission.value < 1000) { return 2 }
  else { return 1 }
})

function convertToCSV(data) {
  const headers = Object.keys(data[0]);
  const rows = data.map(row =>
    headers.map(field => JSON.stringify(row[field], replacer)).join(',')
  );
  return [headers.join(','), ...rows].join('\r\n');
}

function replacer(key, value) {
  return value === null ? '' : value;  // handle nulls
}

function downloadCSV(csvContent, filename = 'BOQ_'+Date.now()+'.csv') {
  const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
  const link = document.createElement("a");

  if (navigator.msSaveBlob) { // for IE
    navigator.msSaveBlob(blob, filename);
  } else {
    const url = URL.createObjectURL(blob);
    link.setAttribute("href", url);
    link.setAttribute("download", filename);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  }
}

function exportboq() {
  downloadCSV(convertToCSV(boq))
}

const fileinput = useTemplateRef('file-input')
function triggerFileInput() {
  fileinput.value.click();
}
function handleFileUpload(event) {
  const file = event.target.files[0];
  if (!file) return;

  Papa.parse(file, {
    header: true,
    skipEmptyLines: true,
    complete: (results) => {
      console.log('Parsed CSV data:', results.data);
      boq.splice(0, Infinity, ...results.data)
    },
    error: (error) => {
      console.error('CSV parsing error:', error);
    }
  });
}

function updatetype(mlist) {
  if (!Object.keys(MaterialData[mlist.material]).includes(mlist.type)) {
    mlist.type = Object.keys(MaterialData[mlist.material])[0]
  }
}
</script>

<template>
  <div class="flex flex-row justify-center rounded bg-white p-3">
    <button title="import csv" class="p-3 cursor-pointer border-e border-e-slate-200 hover:bg-slate-200 rounded" @click="triggerFileInput"><ImportIcon/></button>
    <input
      type="file"
      ref="file-input"
      accept=".csv"
      @change="handleFileUpload"
      class="hidden" />
    <button title="export as csv" class="p-3 cursor-pointer border-e border-e-slate-200 hover:bg-slate-200 rounded" @click="exportboq"><ExportIcon/></button>
    <button title="clear all" class="p-3 cursor-pointer hover:bg-slate-200 rounded" @click="resetboq"><ReloadIcon/></button>
  </div>
  <table class="table-fixed border-collapse p-5 w-full backdrop-blur-lg">
    <thead>
      <tr class="border-b border-b-slate-300">
        <th></th>
        <th class="p-5">Material</th>
        <th class="p-5">Type</th>
        <th class="p-5" colspan="2">Embodied Carbon Factor</th>
        <th class="p-5">Quantity</th>
        <th class="p-5">Emission<br>(kgCO<sub>2</sub>)</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-b border-b-slate-300" v-for="matlist,m in boq">
        <td class="p-5 text-center"><button title="delete row" class="bg-white rounded cursor-pointer p-3 hover:bg-slate-200" @click="deletefromboq(m)"><MinusIcon/></button></td>
        <td class="p-5" :title="matlist.material">
          <select class="bg-slate-200 p-3 rounded w-full" v-model="matlist.material" @change="updatetype(matlist)">
            <option v-for="mat in Object.keys(MaterialData).sort()">{{ mat }}</option>
          </select>
        </td>
        <td class="p-5" :title="matlist.type">
          <select class="bg-slate-200 p-3 rounded w-full" v-model="matlist.type">
            <option v-for="tp in Object.keys(MaterialData[matlist.material]).sort()">{{ tp }}</option>
          </select>
        </td>
        <td class="p-5 text-right">{{ MaterialData[matlist.material][matlist.type]["embodied carbon factor"] }}</td>
        <td class="p-5 text-left">{{ MaterialData[matlist.material][matlist.type]["functional unit"] }}</td>
        <td class="p-5 flex flex-row items-center gap-1" :title="matlist.mass">
          <input class="bg-slate-200 p-3 rounded w-full text-right" type="number" v-model="matlist.mass"></input>
          <div>{{ MaterialData[matlist.material][matlist.type]["functional unit"].split("/")[1] }}</div>
        </td>
        <td 
          class="p-5 text-center truncate"
          :title='(MaterialData[matlist.material][matlist.type]["embodied carbon factor"] * matlist.mass).toFixed(4)'
        >{{ (MaterialData[matlist.material][matlist.type]["embodied carbon factor"] * matlist.mass).toFixed(4) }}</td>
      </tr>
      <tr>
        <td class="text-center p-5">
          <button title="add new row" class="bg-white rounded cursor-pointer p-3 hover:bg-slate-200" @click="addnewtoboq"><PlusIcon/></button>
        </td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td class="text-right p-5 font-bold">Total</td>
        <td class="p-5 font-black text-center truncate" :class="'bg-' + colorseq[totalemissionidx-1] + '-500'" :title="totalemission.toFixed(4)">{{ totalemission.toFixed(4) }}</td>
      </tr>
      <tr>
        <td colspan="6"></td>
        <td class="flex flex-row">
          <div v-for="c in colorseq.toReversed()" :class="'bg-' + c + '-500'" class="grow h-2"></div>
        </td>
      </tr>
    </tbody>
  </table>
</template>