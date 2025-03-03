<script setup lang="ts">
	const props = defineProps({
		width: Number,
		height: Number,
	})

	const cubeContainerSize = computed(() => {
		return { width: `${props.width}px`, height: `${props.height}px` }
	})
</script>

<template>
	<div :style="cubeContainerSize" class="cube-container">
		
	</div>
</template>

<style lang="css" scoped>
	.cube-container {
		background-color: #66ccff;
	}
</style>