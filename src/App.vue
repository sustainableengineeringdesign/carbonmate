<script setup>
import InformationIcon from "vue-material-design-icons/Information.vue"
import CloseIcon from "vue-material-design-icons/Close.vue"
import Calculator from './components/Calculator.vue';
import UserGuide from "./components/UserGuide.vue";
import { ref } from "vue";

const showguide = ref(false)
</script>

<template>
  <div class="flex-0 text-left text-lg font-black flex flex-row">
    <div class="drop-shadow-lg drop-shadow-slate-500 backdrop-blur-lg p-3 rounded">CarbonMaTE</div>
    <div class="grow"></div>
    <button title="user guide" class="bg-white p-3 rounded-full cursor-pointer hover:bg-slate-200 drop-shadow-lg drop-shadow-slate-500" @click="showguide = true"><InformationIcon/></button>
  </div>
  <div class="flex-1 rounded-lg flex flex-col justify-center p-10">
    <div class="h-fit w-full flex flex-col items-center gap-2">
      <Calculator/>
    </div>
  </div>
  <div class="absolute left-0 top-0 w-screen h-screen bg-slate-500/50 backdrop-blur-xs backdrop-grayscale flex flex-col p-10 gap-3" :class="showguide ? '' : 'hidden'">
    <div class="flex flex-row">
      <div class="grow"></div>
      <button title="close" class="bg-white p-3 rounded-full cursor-pointer hover:bg-slate-200" @click="showguide = false"><CloseIcon/></button>
    </div>
    <UserGuide/>
  </div>
</template>