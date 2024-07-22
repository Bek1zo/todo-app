<script setup>

import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";
import {onMounted, provide, ref, watch} from "vue";

const taskList = ref([])

const filteredTaskList = ref([])

const currentPage = ref()


watch(currentPage, (newValue) => {
  if (newValue === null) {
    filteredTaskList.value = taskList.value
  } else {
    filteredTaskList.value = taskList.value.filter((item) => item.status === currentPage.value)
  }
})

const updateFilter = () => {
  console.log(currentPage)
  if (currentPage.value === null) {
    filteredTaskList.value = taskList.value
  } else {
    filteredTaskList.value = taskList.value.filter((item) => item.status === currentPage.value)
  }
}


onMounted(() => {
  taskList.value = JSON.parse(localStorage.getItem('taskList'));
  if (taskList.value === null) {
    taskList.value = []
    localStorage.setItem("taskList", '[]');
  }
  currentPage.value = null
})

const syncStorage = () => {
  localStorage.setItem('taskList', JSON.stringify(taskList.value));
}


provide('syncStorage', syncStorage);

provide("taskList", taskList)

provide("filteredTaskList", filteredTaskList)

provide("currentPage", currentPage)

provide("updateFilter", updateFilter)

</script>

<template>
  <div class="container min-h-dvh flex flex-col m-auto gap-16">
    <Header/>

    <Body/>

    <Footer/>

  </div>

</template>

<style scoped>

</style>
