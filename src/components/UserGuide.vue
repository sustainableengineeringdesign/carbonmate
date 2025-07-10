<script setup>
import { ref } from 'vue';
import MaterialData from '../assets/materials.json'
import ImportIcon from "vue-material-design-icons/Import.vue"
import ExportIcon from "vue-material-design-icons/Export.vue"
import ReloadIcon from "vue-material-design-icons/Reload.vue"
import PlusIcon from "vue-material-design-icons/Plus.vue"
import MinusIcon from "vue-material-design-icons/Minus.vue"

const tabidx = ref(0)
</script>

<template>
  <div class="flex flex-col gap-2 h-full overflow-y-hidden">
    <div class="flex flex-row gap-2">
      <div 
        class="grow text-center rounded p-3 cursor-pointer font-bold" 
        :class="tabidx == 0 ? 'bg-slate-500 hover:bg-slate-500/50 text-white' : 'bg-slate-100/10 hover:bg-slate-100/50'"
        @click="tabidx = 0"
      >How to use CarbonMaTE</div>
      <div 
        class="grow text-center rounded p-3 cursor-pointer bg-slate-100/10 hover:bg-slate-100/50 font-bold" 
        :class="tabidx == 1 ? 'bg-slate-500 hover:bg-slate-500/50 text-white' : 'bg-slate-100/10 hover:bg-slate-100/50'"
        @click="tabidx = 1"
      >Datasheet</div>
    </div>
    <div class="flex flex-row overflow-x-hidden h-full">
      <div class="grow transition-all overflow-y-auto flex flex-col gap-2" :class="tabidx == 0 ? 'w-full' : 'h-0 w-0'">
        <div class="bg-slate-200 rounded p-5">
          <div>
            <span class="font-black">CarbonMaTE</span>: <b>Carbon</b> <b>M</b>easurement <b>a</b>nd <b>T</b>racking <b>E</b>ngine	
            <br>
            The CarbonMaTE tool allows students to calculate the carbon footprint of their design concepts based on the materials they use. 
            This tool helps students assess the environmental impact of their design decisions by quantifying the CO₂ emissions associated with the materials' production processes.
          </div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          <div class="font-bold">Step 1 Input material data</div>
          <div>Material Selection: Students will enter the materials used in their design project. For example, concrete, steel, wood, plastic, aluminum, etc.</div>
          <div>Material Mass: Students will input the quantity (in respective unit) of each material used in their design.</div>
          <div class="h-5"></div>
          <div>
            Use <button class="bg-white rounded cursor-pointer p-3 align-middle"><PlusIcon/></button> and <button class="bg-white rounded cursor-pointer p-3 align-middle"><MinusIcon/></button> to add or remove row.
            Use <button class="bg-white rounded cursor-pointer p-3 align-middle"><ReloadIcon/></button> to remove all existing rows.
          </div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          <div class="font-bold">Step 2: Calculate CO₂ Emissions</div>
          <div>
            The emission factor (kg CO₂e per kg of material) is used to calculate how much CO₂ is emitted during the production of each material. 
            The basic formula for calculating CO<sub>2</sub> emissions is:
          </div>
          <div class="text-center">
            Emissions (kg CO<sub>2</sub>) = Mass of Material (kg) &times; Emission Factor (kg CO<sub>2</sub>e/kg)
          </div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          <div>For example:</div>
          <div>If you use 100 kg of concrete, and the emission factor for concrete is 0.15 kg CO<sub>2</sub>e per kg, the emissions will be:</div>
          <div class="text-center">Emissions = 100kg &times; 0.15kg CO<sub>2</sub>e/kg = 15 kg CO<sub>2</sub></div>
          <div>After calculating the CO<sub>2</sub> emissions for each material, students will sum the total emissions for their design project:</div>
          <div class="text-center">Total Emissions (kg CO<sub>2</sub>) = &sum;(Emissions of each material)</div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          <div>
            Use <button class="bg-white rounded cursor-pointer p-3 align-middle"><ExportIcon/></button> to export the material list to a local CSV file.
            Use <button class="bg-white rounded cursor-pointer p-3 align-middle"><ImportIcon/></button> to import the exported CSV file containing the material list.
          </div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          <div>Based on the total emissions, students will get a Carbon Score using the following scale:</div>
          <div class="flex flex-row justify-center p-2">
            <table class="table-auto w-auto">
              <thead>
                <tr class="bg-slate-500 text-white">
                  <th class="p-2">Total Emissions (kg CO<sub>2</sub>)</th>
                  <th class="p-2" colspan="2">Carbon Score</th>
                </tr>
              </thead>
              <tbody>
                <tr class="bg-green-500">
                  <td class="text-center p-2">&lt; 100 kg</td>
                  <td class="text-center p-2">Excellent (5)</td>
                  <td class="text-center p-2">[90%, 100%]</td>
                </tr>
                <tr class="bg-lime-500">
                  <td class="text-center p-2">100 - 300 kg</td>
                  <td class="text-center p-2">Good (4)</td>
                  <td class="text-center p-2">[70%, 90%)</td>
                </tr>
                <tr class="bg-amber-500">
                  <td class="text-center p-2">301 - 600 kg</td>
                  <td class="text-center p-2">Average (3)</td>
                  <td class="text-center p-2">[50%, 70%)</td>
                </tr>
                <tr class="bg-orange-500">
                  <td class="text-center p-2">601 - 1000 kg</td>
                  <td class="text-center p-2">Poor (2)</td>
                  <td class="text-center p-2">[30%, 50%)</td>
                </tr>
                <tr class="bg-red-500">
                  <td class="text-center p-2">&gt; 1000 kg</td>
                  <td class="text-center p-2">Very Poor (1)</td>
                  <td class="text-center p-2">[0%, 30%)</td>
                </tr>
              </tbody>
            </table>
          </div>
          <div>The Carbon Score reflects how sustainable the design is, with lower emissions resulting in a better score.</div>
          <div><b>Note:</b> In mathematical notation, square brackets [ ] are used to indicate that the endpoint(s) of an interval are included in the solution set, representing "less than or equal to" (&le;) or "greater than or equal to" (&ge;) when used in inequalities. Conversely, parentheses ( ) indicate that the endpoint(s) are excluded, representing "less than" (&lt;) or "greater than" (&gt;). </div>
        </div>
        <div class="bg-slate-200 rounded p-5">
          Carbon data sources: <a href="https://www.cidb.gov.my/wp-content/uploads/2022/11/V4_EMBODIED-CARBON-INVENTORY-TEMPLATE-final-1.pdf" target="_blank">https://www.cidb.gov.my/wp-content/uploads/2022/11/V4_EMBODIED-CARBON-INVENTORY-TEMPLATE-final-1.pdf</a>
        </div>
      </div>
      <div class="grow transition-all overflow-y-auto flex flex-col gap-2 px-2" :class="tabidx == 1 ? 'w-full' : 'h-0 w-0'">
        <div class="bg-slate-200 rounded p-5" v-for="mat in Object.keys(MaterialData).sort()">
          <div class="font-black">{{ mat }}</div>
          <table class="table-fixed w-full">
            <thead>
              <tr>
                <th>Type</th>
                <th>Market Price</th>
                <th>Embodied Carbon Factor</th>
                <th>Remark</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="mtype in Object.keys(MaterialData[mat]).sort()" class="hover:bg-slate-300">
                <td class="p-2">{{ mtype }}</td>
                <td class="p-2 text-center">{{ MaterialData[mat][mtype]["market price"] }}</td>
                <td class="p-2 text-center">{{ MaterialData[mat][mtype]["embodied carbon factor"] }}&nbsp;{{ MaterialData[mat][mtype]["functional unit"] }}</td>
                <td class="p-2">{{ MaterialData[mat][mtype]["remark"] }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>