<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import GISMap from './views/GISMap.vue';
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <a href="https://vuejs.org/" target="_blank">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
      </a>

    </div>
    <div class="row">
      <!-- <HelloWorld msg="Vite + Vue" /> -->
      <GISMap />
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