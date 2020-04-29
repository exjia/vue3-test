<template>
  <div class="hello">
    <h1>name:{{ state.name }} wechart:{{ state.wechart }}</h1>
    <div v-for="(user, index) in state.users" :key="index">
      <p>{{ user.name }}</p>
      <p>{{ user.email }}</p>
    </div>
    <button @click="fetchData()">获取数据</button>
  </div>
</template>

<script>
import { reactive, computed, onMounted } from 'vue'
import axios from 'axios'
export default {
  setup() {
    const state = reactive({
      name: 'test',
      wechart: '2131321',
      users: []
    })

    onMounted(() => {
      fetchData()
    })

    function fetchData() {
      axios.get('http://jsonplaceholder.typicode.com/users').then(res => {
        state.users = res.data
      })
    }

    return {
      state,
      fetchData
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
