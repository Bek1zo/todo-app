<script setup>

import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";
import {onMounted, provide, ref} from "vue";

const taskList = ref([{}])


onMounted(() => {
  taskList.value = JSON.parse(localStorage.getItem('taskList'));
  console.log(taskList.value === null)
  if (taskList.value === null) {
    console.log(taskList.value)
    localStorage.setItem("taskList", '[]');
  }
})

provide("taskList", taskList)

</script>

<template>
  <div class="container min-h-dvh flex flex-col m-auto gap-20">
    <Header/>

    <Body/>

    <Footer/>

  </div>

</template>

<style scoped>

</style>
