<script setup>
import { ref } from 'vue';
import MaterialData from '../assets/materials.json'

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
        <div class="bg-slate-200 rounded p-5">fdasfkh</div>
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
        geoifo8gfuoi <br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf<br/> fdsafasf
      </div>
    </div>
  </div>
</template>