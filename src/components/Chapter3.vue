<template>
  <div class="chapter3">
    <p>Computed Data: {{ computedData }}</p>
    <p>Computed Data: {{ computedData }}</p>
    <p>Methods Data: {{ methodsData() }}</p>
    <p>Methods Data: {{ methodsData() }}</p>
  </div>
</template>

<script lang='ts'>
  import Vue from 'vue'
  
  const data : {
    randData :number
  } = {
    randData: 0
  }
  
  export default Vue.extend({
    name: "Chapter3",
    data() {
      return data
    },
    computed: {
      computedData() {
        return Math.random()
      }
    },
    methods: {
      methodsData() {
        return Math.random()
      }
    }
  })
</script>

<style scoped>

</style>