<template>
  <div class="chapter2">
    <h1>Chapter 2</h1>
    <div class="increment-number">
      <h2>{{ title.increment }}</h2>
      <p>{{ count }} times clicked!</p>
      <button @click="increment">Increment!</button>
      <button @click="reset">Reset...</button>
    </div>
    <div class="svg-control">
      <h2>{{ title.svgControl }}</h2>
      <div>
        <svg xmlns="http://www.w3.org/2000/svg" version="1.1" viewport="0,0" width="200" height="200">
          <circle cx="100" cy="100" :r="radius" fill="#08a" />
        </svg>
      </div>
      <div>
        <input type="range" min="10" max="100" v-model="radius">
      </div>
    </div>
    <div class="array-control">
      <h2>{{ title.monster }}</h2>
      <div class="addMonster">
        <label>
          名前:
          <input type="text" v-model="name" placeholder="ゴーレム">
        </label>
        <button @click="addMonster">Add</button>
      </div>
      <ul>
        <li v-for="(item, index) in monsterList" :key="item.id" v-if="item.hp">
          ID.{{ item.id }} {{ item.name }} HP.{{ item.hp }}
          <span class="dying" v-if="item.hp < 50">瀕死！</span>
          <button @click="attackMonster(index)">Attack!</button>
          <button @click="removeMonster(index)">remove</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang='ts'>
  import Vue from 'vue'
  import axios from 'axios'
  
  const data : {
    title: {
      increment: string,
      svgControl: string,
      monster: string
    },
    count: number,
    radius: number,
    monsterList: {
      id: number,
      name: string,
      hp: number,
    }[],
    name: string
  } = {
    title: {
      increment: 'Increment number with button click!',
      svgControl: 'Change circle radius.',
      monster: 'List of Monsters'
    },
    count: 0,
    radius: 50,
    monsterList: [],
    name: ''
  }
  
  export default Vue.extend({
    name: "Chapter2",
    data() {
      return data
    },
    async created() {
      const res :any = await axios.get('monsterList.json').catch(e => {
        console.error(e)
      })
      this.monsterList = res.data
    },
    methods: {
      increment() :void {
        this.count += 1
      },
      reset() :void {
        this.count = 0
      },
      addMonster()  :void {
        let max :any = this.monsterList.reduce((a:any,b:any) => {
          return a.id > b.id ? a.id : b.id
        })
        let hp :number = Math.trunc(Math.random()*1000)
        this.monsterList.push({
          id: max + 1,
          name: this.name,
          hp
        })
      },
      attackMonster(index:number) :void {
        const target = this.monsterList[index]
        target.hp -= Math.trunc(Math.random()*20)
        if (target.hp <= 0) {
          target.hp = 0
        }
      },
      removeMonster(index:number) :void {
        this.monsterList.splice(index, 1)
      }
    }
  })
</script>

<style lang='scss' scoped>
  li {
    list-style: none;
  }
  p {
    font-size: 24px;
  }
  .chapter2 {
    padding: 0 0 50px;
  }
</style>