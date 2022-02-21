<template>
	<div class="TodoDoneList">

	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
	name: 'TodoListDone',
	props: {
		DoneList: {
			type: Array,
			required: true
		}
	},

	setup() {
	},
})
</script>