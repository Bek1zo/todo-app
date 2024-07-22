<script setup>
import {inject} from "vue";

const taskList = inject('taskList')
const syncStorage = inject('syncStorage')

const makeStringData = (today) => {
  const yyyy = today.getFullYear();
  let mm = today.getMonth() + 1; // Months start at 0!
  let dd = today.getDate();

  if (dd < 10) dd = '0' + dd;
  if (mm < 10) mm = '0' + mm;

  const formattedToday = today.getHours() + ':' + today.getMinutes() + ' ' + dd + '.' + mm + '.' + yyyy + ' г.';

  return formattedToday
}

const changeTaskStatus = (task) => {
  taskList.value.map((item) => {
    if (item.date === task.date) {
      item.status = task.status;
    }
  })
  syncStorage()
}

</script>

<template>
  <ul class="flex flex-col gap-2">
    <li v-for="task in taskList" class="flex justify-between border-2 gap-20 p-2">
      <div class="w-1/12">
        <input type="checkbox" v-model="task.status" @change="changeTaskStatus(task)">
      </div>
      <div class="w-10/12 flex justify-start">
        {{ task.name }}
      </div>
      <div class="w-2/12 flex justify-end">
        {{ makeStringData(new Date(task.date)) }}
      </div>
    </li>
  </ul>
</template>

<style scoped>

</style>