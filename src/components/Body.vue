<script setup>


import {inject, ref, watch, watchEffect} from "vue";
import List from "./BodyComponent/List.vue";

const taskList = inject('taskList')
const filteredTaskList = inject('filteredTaskList')
const syncStorage = inject('syncStorage')
const currentPage = inject('currentPage')
const updateFilter = inject('updateFilter')

const taskName = ref('')

const addTodo = () => {
  taskList.value.push({
    name: taskName.value,
    status: false,
    date: new Date()
  })
  taskName.value = ''
  syncStorage()
}

const clearCompletedTask = () => {
  taskList.value = taskList.value.filter((item) => item.status !== true)
  updateFilter()
  syncStorage()
}



</script>

<template>
<div class="flex flex-col w-full border-2 p-5 gap-5 shadow-2xl">
  <div class="flex flex-col gap-1">
    <div class="flex border-2 justify-center items-center drop-shadow-sm">
      <input type="text" class="w-full h-12 border-2 p-2 font-mono " @keydown.enter="addTodo" v-model="taskName">
      <span class="w-24 text-center cursor-pointer" @click="addTodo">Добавить</span>
    </div>
    <div class="text-center text-xs">Введи название задачи</div>
  </div>

  <List/>

  <div class="flex gap-6 mr-2 justify-end">
    <div class="rounded-full border-2 w-auto p-2 text-center cursor-pointer" @click="currentPage = null">Все</div>
    <div class="rounded-full border-2 w-auto p-2 text-center cursor-pointer" @click="currentPage = false">Активные</div>
    <div class="rounded-full border-2 w-auto p-2 text-center cursor-pointer" @click="currentPage = true">Завершенные</div>
  </div>
  <div class="text-xs font-mono tracking-widest text-end mr-2 cursor-pointer" @click="clearCompletedTask">
    Очистить завершенные задачи
  </div>
</div>
</template>

<style scoped>

</style>