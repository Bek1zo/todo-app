<script setup>


import {computed, inject, ref, watchEffect} from "vue";

const taskList = inject('taskList')

const taskName = ref('')

const addTodo = () => {
  console.log(taskName)
  console.log(typeof(taskList.value))
  taskList.value.push({
    name: taskName.value,
    status: false
  })
}


</script>

<template>
<div class="flex flex-col w-full border-2 p-5 gap-5 shadow-2xl">
  <div class="flex flex-col gap-1">
    <div class="flex border-2 justify-center items-center drop-shadow-sm">
      <input type="text" class="w-full h-12 border-2 p-2 font-mono " v-model="taskName">
      <span class="w-24 text-center cursor-pointer" @click="addTodo" @keydown="addTodo">Добавить</span>
    </div>
    <div class="text-center text-xs">Введи название задачи</div>
  </div>

  <ul>
    <li v-for="task in taskList" class="flex border-2">
      <div>
        <input type="radio" v-model="task.status">
      </div>
      <div>
        {{ task.name }}
      </div>
    </li>
  </ul>
</div>
</template>

<style scoped>

</style>