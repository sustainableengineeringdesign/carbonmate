<script setup>
import HelloWorld from './components/HelloWorld.vue'
import InformationIcon from "vue-material-design-icons/Information.vue"
import Calculator from './components/Calculator.vue';
</script>

<template>
  <div class="flex-0 text-left text-lg font-black flex flex-row">
    CarbonMaTE
    <div class="grow"></div>
    <button><InformationIcon></InformationIcon></button>
  </div>
  <div class="flex-1 rounded-lg flex flex-col justify-center p-10">
    <div class="h-fit w-full flex flex-col items-center gap-2">
      <Calculator/>
    </div>
  </div>
  <!-- <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" /> -->
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
