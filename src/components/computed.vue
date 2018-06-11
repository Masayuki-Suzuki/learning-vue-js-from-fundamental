<template lang="pug">
  .computed
    .searchForm
      label.searchForm__input
        input(v-model.number="budget" type="number")
        | 円以下に絞り込む
      label.searchForm__input
        input(v-model.number="limit" type="number")
        | 件を表示
    p.result {{ matched.length }} 件中、 {{ limited.length }} 件を表示中
    div
      button(@click="order=!order") 切り替え
    ul.itemList
      li.itemList__item(v-for="item in limited" :key="item.id")
        |{{ item.name }}: {{ item.price }} 円
</template>

<script lang="ts">
  import Vue from 'vue'
  import _ from 'lodash'

  interface listData {
    id :number,
    name :string,
    price :number
  }

  interface mainData {
    title :string,
    budget :number,
    limit :number,
    order :boolean,
    list :listData[]
  }

  const data :mainData = {
    title: 'Chapter 4',
    budget: 300,
    limit: 2,
    order: false,
    list: [
      { id: 1, name: 'りんご', price: 100},
      { id: 2, name: 'ばなな', price: 50},
      { id: 3, name: 'いちご', price: 500},
      { id: 4, name: 'オレンジ', price: 200},
      { id: 5, name: 'メロン', price: 1000},
    ]
  }

  export default Vue.extend({
    name: "Computed",
    data() {
      return data
    },
    computed: {
      matched() :{}[] {
        return this.list.filter(el => {
          // less than equal. *not arrow!!
          return el.price <= this.budget
        }, this)
      },
      sorted() :{}[] {
        return _.orderBy(this.matched, 'price', this.order ? 'desc' : 'asc')
      },
      limited() :{}[] {
        return this.sorted.slice(0, this.limit)
      }
    }
  })
</script>

<style lang="scss" scoped>
  li {
    list-style: none;
  }
  .computed {
    padding: 0 0 50px;
  }
  .searchForm {
    display: flex;
    justify-content: space-between;
    margin: 0 auto;
    width: 35vw;
    &__input {
      text-align: left;
      input {
        border: solid 1px #ccc;
        border-radius: 4px;
        font-size: 14px;
        margin: 0 10px 0 0;
        padding: 10px;
      }
    }
  }
</style>
