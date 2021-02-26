<template>
  <div>
    <div class="">用戶訊息</div>
    <button
      v-for="item of btnKey" 
      :key="`btn${item.key}`"
      @click="sortName(item.sort)">{{item.name}}</button>
    <ul>
      <li v-for="(item, index) of listName" :key="`list${index}}`">{{item.name}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      userList: [],
      btnKey: [
        {sort: 'asc', name:'升序', key: 1},
        {sort: 'desc', name:'降序', key: 2},
        {sort: 'no', name:'重置', key: 3},
      ],
      key: ''
    }
  },
  computed: {
    listName () {
      let list = []
      if (this.key == 'asc') {
        list = [].concat(this.userList).sort((a, b)=> a.name > b.name ? 1 : -1)
      } else if (this.key == 'desc') {
        list = [].concat(this.userList).sort((a, b)=> b.name > a.name ? 1 : -1)
      } else {
        list = this.userList
      }
      return list
    }
  },
  created () {
    this.getListapi()
  },
  methods: {
    async getListapi () {
      //解構賦值
      const {data} = await axios.get('https://jsonplaceholder.typicode.com/users')
      this.userList = data
    },
    sortName (sort) {
      this.key = sort
    }
  }
}
</script>

<style>
ul {
  list-style: none;
  padding: 0;
}
li {
  padding: 0;
}
</style>