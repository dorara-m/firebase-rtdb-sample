<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

// import HelloWorld from './components/HelloWorld.vue'

const items = [
  {
    name: 'アイテム1',
    date: '20201-10-14',
    checked: false
  },
  {
    name: 'アイテム2',
    date: '20201-10-14',
    checked: true
  }
]
</script>

<template>
  <h1>シンプルなTodoリスト</h1>
  <p>firebaseとリアルタイムで連携します。</p>
  <ul>
    <li v-for="item,index in items" :key="index">
      <input type="checkbox" name="" id="" v-model="item.checked">
      <span>{{ item.name }}</span>
    </li>
  </ul>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
li {
  padding: 20px;
  border: 1px solid #bbb;
  margin-top: 10px;
}
</style>
