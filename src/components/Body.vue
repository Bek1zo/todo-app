<script setup>


import {inject, ref, watch, watchEffect} from "vue";
import List from "./BodyComponent/List.vue";

const taskList = inject('taskList')

const taskName = ref('')

const addTodo = () => {
  taskList.value.push({
    name: taskName.value,
    status: false,
    date: new Date()
  })
  taskName.value = ''
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
</div>
</template>

<style scoped>

</style>