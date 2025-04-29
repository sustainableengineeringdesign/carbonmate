<script setup>
import ImportIcon from "vue-material-design-icons/Import.vue"
import ExportIcon from "vue-material-design-icons/Export.vue"
import ReloadIcon from "vue-material-design-icons/Reload.vue"
import PlusIcon from "vue-material-design-icons/Plus.vue"
</script>

<template>
  <div class="flex flex-row gap-2 justify-center">
    <button title="import csv"><ImportIcon/></button>
    <button title="export as csv"><ExportIcon/></button>
    <button title="clear all"><ReloadIcon/></button>
  </div>
  <table class="table-fixed border-collapse p-5 w-full backdrop-blur-lg">
    <thead>
      <tr class="border-b border-b-slate-300">
        <th class="p-5">Material</th>
        <th class="p-5">Specification</th>
        <th class="p-5">Embodied Carbon Factor<br>kgCO<sub>2</sub>e/kg</th>
        <th class="p-5">Mass<br>(kg)</th>
        <th class="p-5">Emission<br>(kgCO<sub>2</sub>)</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-b border-b-slate-300">
        <td class="p-5"><select class="bg-slate-200 p-2 rounded w-full"><option>a</option><option>b</option></select></td>
        <td class="p-5"><select class="bg-slate-200 p-2 rounded w-full"><option>a</option><option>b</option></select></td>
        <td class="p-5">5423542</td>
        <td class="p-5"><input class="bg-slate-200 p-2 rounded w-full" type="number"></input></td>
        <td class="p-5">52423545</td>
        <!-- <td class="p-5">Specification</td> -->
        <!-- <td class="p-5">Embodied Carbon Factor<br>kgCO<sub>2</sub>e/kg</td> -->
        <!-- <td class="p-5">Mass<br>(kg)</td> -->
        <!-- <td class="p-5">Emission<br>(kgCO<sub>2</sub>)</td> -->
      </tr>
      <tr>
        <td class="text-center p-5">
          <button><PlusIcon/></button>
        </td>
        <td></td>
        <td></td>
        <td class="text-right p-5 font-bold">Total</td>
        <td class="p-5 font-black">1235415234352</td>
      </tr>
    </tbody>
  </table>
</template>