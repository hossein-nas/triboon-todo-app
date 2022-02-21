<template>
<div class="AddNew">
	<form >
		<input type="text" name="TaskName" v-model="taskTitle" >
    <select v-model="taskPriority" name="taskPriority">
      <option> --Select-- </option>
      <option value="1"> Low </option>
      <option value="2"> Medium </option>
      <option value="3"> High </option>
    </select>
    <select v-model="taskColor" name="taskColor">
      <option> --Select Color-- </option>
      <option value="red">Red</option>
      <option value="blue">Blue</option>
      <option value="orange">Orange</option>
      <option value="green">Green</option>
      <option value="yellow">Yellow</option>
    </select>
    <button type="submit" @click.prevent="handleSubmit">Add Task </button>
	</form>
</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'AddNew',

  emits: ['added-task'],

  setup (props, { emit }) {
    const taskTitle = ref<string>('')
    const taskPriority = ref<number>()
    const taskColor = ref<string>()

    const handleSubmit = () => {
      emit('added-task', {
        title: taskTitle.value,
        color: taskColor.value,
        priority: taskPriority.value
      })
    }

    return {
      taskTitle,
      taskPriority,
      taskColor,
      handleSubmit
    }
  }
})
</script>
