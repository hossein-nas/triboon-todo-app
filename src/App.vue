<script setup lang="ts">
import { ref } from '@vue/reactivity'
import TodoList from './components/TodoList.vue'
import AddNewTodo from './components/AddNewTodo.vue'

const taskList = ref<object[]>([])
const taskDoneList = ref<object[]>([])

const addNewTask = (payload: object) => {
  taskList.value.push({
    id: taskList.value.length,
    ...payload
  })
}
</script>

<template>
<div class="TodoApp">
  <add-new-todo @added-task="addNewTask" />
  <todo-list :TodoList="taskList"></todo-list>
</div>
</template>

<style lang="less">
body, html {
   font-size: 16px;
   padding: 0;
   margin: 0;
}
#app {
}
</style>
