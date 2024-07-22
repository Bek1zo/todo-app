<script setup>
import {inject} from "vue";

const taskList = inject('taskList')

const makeStringData = (today) => {
  const yyyy = today.getFullYear();
  let mm = today.getMonth() + 1; // Months start at 0!
  let dd = today.getDate();

  if (dd < 10) dd = '0' + dd;
  if (mm < 10) mm = '0' + mm;

  const formattedToday = today.getHours() + ':' + today.getMinutes() + ' ' + dd + '.' + mm + '.' + yyyy + ' г.';


  return formattedToday
}

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
      <div class="flex justify-end">
        {{ makeStringData(new Date(task.date)) }}
      </div>
    </li>
  </ul>
</template>

<style scoped>

</style>