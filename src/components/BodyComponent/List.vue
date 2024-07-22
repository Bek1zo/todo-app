<script setup>
import {inject, ref, watch} from "vue";

const taskList = inject('taskList')
const filteredTaskList = inject('filteredTaskList')
const syncStorage = inject('syncStorage')
const updateFilter = inject('updateFilter')

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

  filteredTaskList.value.map((item) => {
    if (item.date === task.date) {
      item.status = task.status;
    }
  })

  taskList.value.map((item) => {
    if (item.date === task.date) {
      item.status = task.status;
    }
  })
  updateFilter()
  syncStorage()
}



</script>

<template>
  <ul class="flex flex-col gap-2">
    <li v-for="task in filteredTaskList" class="flex justify-between border-2 gap-20 p-2">
      <div class="w-8">
        <input class="w-8 h-8" type="checkbox" v-model="task.status" @change="changeTaskStatus(task)">
      </div>
      <div class="w-10/12 flex justify-start items-center">
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