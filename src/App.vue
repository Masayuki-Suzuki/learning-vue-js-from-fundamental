<template>
  <div id="app">
    <Chapter2></Chapter2>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Chapter2 from './components/Chapter2.vue'

export default Vue.extend({
  name: 'app',
  components : {
    Chapter2
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
