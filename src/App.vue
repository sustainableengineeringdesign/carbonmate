<script setup>
import InformationIcon from "vue-material-design-icons/Information.vue"
import Calculator from './components/Calculator.vue';
</script>

<template>
  <div class="flex-0 text-left text-lg font-black flex flex-row">
    <div class="hover:drop-shadow-lg drop-shadow-slate-500">CarbonMaTE</div>
    <div class="grow"></div>
    <button title="user guide"><InformationIcon/></button>
  </div>
  <div class="flex-1 rounded-lg flex flex-col justify-center p-10">
    <div class="h-fit w-full flex flex-col items-center gap-2">
      <Calculator/>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
