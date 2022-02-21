<template>
<div class="TaskItem">
	<div class="title">
		{{ item.title }}
	</div>
	<div class="priority">
	(priority: {{ item.priority }})
	</div>
	<div class="color" :style="{'--task-color' : item.color }">
		<span class="col" ></span>
	</div>

	<button @click.prevent="markDone">Mark Done</button>
	<button @click.prevent="pinTask">Pin Task</button>
</div>

</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    item: {
      type: Object,
      required: true
    }
  },

  emits: ['mark-done', 'pin-task'],
  setup (props, { emit }) {
    const pinTask = () => {
      emit('pin-task', props.item.id)
    }

    const markDone = () => {
      emit('mark-done', props.item.id)
    }

    return {
      pinTask,
      markDone
    }
  }
})
</script>

<style scoped lang="less">
.TaskItem{
	padding: 2rem;
	display: flex;
	gap: 1rem;
	align-items: center;

		.title{
			font-size: 2rem;
		}
		.priority{
		}

	.color {
		span{
			display: block;
			width: 1.5em;
			height: 1.5rem;
			background-color: var(--task-color);
		}
	}
}
</style>
