<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Calculator from "./components/Calculator.vue";

export default Vue.extend({
  name: "App",
  components: {
    Calculator,
  },
});
</script>

<style>
body {
  margin: 0%;
  padding: 0%;
  background-color: rgb(31, 31, 31);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
