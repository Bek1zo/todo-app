<script setup>
import {inject} from "vue";

const taskList = inject('taskList')
</script>

<template>
  <ul class="flex flex-col gap-2">
    <li v-for="task in taskList" class="flex border-2 gap-20 p-2">
      <div>
        <input class="checked:bg-no-repeat checked:bg-center checked:border-indigo-500 checked:bg-indigo-100" type="radio" v-model="task.status">
      </div>
      <div>
        {{ task.name }}
      </div>
    </li>
  </ul>
</template>

<style scoped>

</style>