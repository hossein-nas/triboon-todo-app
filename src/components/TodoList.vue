<template>
<div class="TodoList">
	<div class="PinedTasks">
		<h1>Pinned Task</h1>
		<task-item :item="item" :key="ind" v-for="(item, ind) in pinnedList" class="pinned" @mark-done="markDone"  />
	</div>
	<div class="Tasks">
		<h1>UnPinned Task</h1>
	<task-item :item="item" :key="ind" v-for="(item, ind) in unpinnedList" @pin-task="pinTask" @mark-done="markDone" />
	</div>

	<div class="DoneTask">
		<h1>Done Task</h1>
	<task-item :item="item" :key="ind" v-for="(item, ind) in doneList" />
	</div>
</div>
</template>

<script lang="ts">
import { computed, defineComponent, onBeforeMount, onMounted, ref, watch } from 'vue'
import TaskItem from './TaskItem.vue'

export default defineComponent({
  name: 'TodoList',
  components: {
    TaskItem
  },
  props: {
    TodoList: {
      type: Array,
      required: true
    }
  },

  setup (props) {
    const localList = ref<object[]>([])

    const pinnedList = computed(() => {
      return localList.value.filter((item: any) => item.pinned)
        .sort((a: any, b:any) => a.priority - b.priority)
        .reverse()
    })

    const unpinnedList = computed(() => {
      return localList.value.filter((item: any) => !item.pinned && !item.done)
        .sort((a: any, b:any) => a.priority - b.priority)
        .reverse()
    })

    const doneList = computed(() => {
      return localList.value.filter((item: any) => item.done)
        .sort((a: any, b:any) => a.priority - b.priority)
        .reverse()
    })

    watch(props.TodoList, () => {
      initLocalList()
    })

    function initLocalList (): void {
      const newItems = props.TodoList.filter((item: any) => {
        const newItemId = item.id
        if (localList.value.find((item:any) => item.id === newItemId)) {
          return false
        }
        return true
      })
      localList.value.push(
        ...newItems.map((item: object) => {
          return {
            ...item,
            done: false,
            pinned: false
          }
        })
      )
    }

    const pinTask = (taskId: any) => {
      const found: any = localList.value.find((item: any) => item.id === taskId)
      found.pinned = true
    }

    const markDone = (taskId: any) => {
      const found: any = localList.value.find((item: any) => item.id === taskId)
      found.done = true
      found.pinned = false
    }
    return {
      localList,
      pinnedList,
      unpinnedList,
      doneList,
      pinTask,
      markDone
    }
  }
})
</script>
