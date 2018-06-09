<template>
  <div class="capture1">
    <transition>
      <p v-if="show">{{ message }}</p>
    </transition>
    <label>
      <input type="checkbox" v-model="show" placeholder="input text">
      <span v-if="show">Hidden Message.</span>
      <span v-if="!show">Show Message.</span>
    </label>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    name: "Chapter1",
    data () {
      return {
        message: 'Hello Vue.js + Typescript!',
        show: true
      }
    }
  })
</script>

<style lang="scss" scoped>
  .v-enter-active,
  .v-leave-active {
    transition: opacity 1s;
  }
  .v-enter,
  .v-leave-to {
    opacity: 0;
  }
</style>
