<script setup lang="ts">
import { ref } from 'vue'
import axios from "axios";
defineProps<{ msg: string }>()

const message = ref("")
const count = ref(0)
const list = ref([]);
const getList = async function (){
  const { data } =await axios.get("https://gorest.co.in/public/v2/todos");
  list.value = data;
}
const add =() =>
  count.value++

</script>

<template>
  <h1>{{ msg + ' ' + message }}</h1>
  <div v-for="(item, index) in list" :key="index">
    <div
    class="border-gray-200 bg-white px-10 py-10 text-sart my-10 rounded-xl"
    >
    <h3 class="text-base font-semibold leading-6 text-gray-900">
      Title : {{ item["title"] }}
    </h3>
    <h3 class="text-base font-semibold leading-6 text-gray-900">
      User : {{ item["user_id"] }}
    </h3>
    <h3 class="text-base font-semibold leading-6 text-gray-900">
      Status : {{ item["status"] }}
    </h3>
    </div>
  </div>

<!-- <pre>{{ list }}</pre> -->
  <div class="card">
    <input type="text" v-model="message">
    <button type="button" @click="$event =>getList()" class="bg-red-400">GET LIST</button>
    <button type="button" @click="count++" class="bg-green-400">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite +  starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
