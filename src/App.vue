<template>
  <div id="app">
    <Chapter1></Chapter1>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Chapter1 from './components/Chapter1.vue'

export default Vue.extend({
  name: 'app',
  components : {
    Chapter1
  }
});
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
