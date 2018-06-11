<template lang="pug">
  .chapter4
    h1 {{ title }}
    div
      label.toggle
        input(type="checkbox" v-model="toggle")
        span(:class="!toggle && 'active'") Computed
        span(:class="toggle && 'active'") Watch
    Computed(v-if="!toggle")
    Watch(v-if="toggle")
</template>

<script lang="ts">
  import Vue from 'vue'
  import Computed from './computed.vue'
  import Watch from './watch.vue'

  const data :{
    title :string
    toggle: boolean,
  } = {
    title: 'Chapter4',
    toggle: false,
  }

  export default Vue.extend({
    name: "Chapter4",
    data() {
      return data
    },
    computed: {
      current() :string {
        return this.toggle ? 'Watch' : 'Computed'
      }
    },
    components: {
      Computed,
      Watch,
    }
  })
</script>

<style lang="scss" scoped>
  .toggle {
    background: #ccc;
    border-radius: 6px;
    display: flex;
    justify-content: space-between;
    margin: 0 auto 40px;
    padding: 5px;
    width: 180px;
    span {
      color: #444;
      font-weight: 600;
      font-size: 12px;
      text-align: center;
      text-transform: uppercase;
      padding: 10px 0;
      width: 90px;
      &.active {
        background: #eee;
        border-radius: 3px;
        color: #666;
      }
    }
    input {
      display: none;
    }
  }
</style>
