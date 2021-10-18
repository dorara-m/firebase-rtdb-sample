<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

// vue基本形
import { reactive } from '@vue/reactivity';
// firebase系
import firebaseKey from './firebaseKey'
import { initializeApp } from 'firebase/app'
import { getDatabase, ref, set, onValue } from "firebase/database";
// コンポーネント系
// import HelloWorld from './components/HelloWorld.vue'

// データ
const state = reactive({
  items: {}
})

const app = initializeApp(firebaseKey)
const db = getDatabase(app)
const itemsRef = ref(db, '/')
// refが更新されたらitemsも更新。事実上firebaseが更新されたら動く関数
onValue(itemsRef, (snapshot) => {
  state.items = snapshot.val();
  console.log('items updated', state.items)
});

// firebaseにデータをセットする関数
function saveItems() {
  const db = getDatabase()
  set(ref(db, '/'), state.items)
}
</script>

<template>
  <h1>シンプルなTodoリスト</h1>
  <p>firebaseとリアルタイムで連携します。</p>
  <ul>
    <li v-for="item,key in state.items" :key="key">
      <input type="checkbox" name="" id="" v-model="item.checked" @change="saveItems">
      <span>{{ item.name }}</span>
    </li>
  </ul>
  <button @click="saveItems">firebaseを手動更新</button>
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
button {
  margin-top: 20px;
}
</style>
