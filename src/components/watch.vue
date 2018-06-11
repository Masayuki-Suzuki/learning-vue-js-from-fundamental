<template lang="pug">
  .watch
    select(v-model="current")
      option(v-for="topic in topics" :value="topic.value")
        | {{ topic.name }}
    div(v-for="item in list")
      | {{ item.full_name }}
</template>

<script lang="ts">
  import Vue from 'vue'
  import axios from 'axios'

  interface topicsType {
    value :string,
    name :string
  }

  const data :{
    list :any[],
    current :string,
    topics :topicsType[]
  } = {
    list: [],
    current: '',
    topics: [
      { value: 'vue', name: 'Vue.js' },
      { value: 'node', name: 'Node.js' },
      { value: 'react', name: 'React.js' },
      { value: 'angular', name: 'Angular' },
      { value: 'jQuery', name: 'jQuery' },
    ]
  }

  export default Vue.extend({
    name: "watch",
    data() {
      return data
    },
    watch: {
      async current(val) {
        console.log(val)
        const res = await axios.get('https://api.github.com/search/repositories', {params: {q: `topic:${val}`}}).catch(err => {
          console.error(err)
          throw new Error(err)
        })
        console.log(res.data.items)
        this.list = res.data.items
        console.log(this.list)
      }
    }
  })
</script>

<style scoped>

</style>
