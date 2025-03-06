<script setup lang="ts">
	const props = defineProps({
		width: {
			type: Number,
			required: true,
		},
		height: {
			type: Number,
			required: true,
		},
	})

	const cubeContainerSize = computed(() => {
		return { width: `${props.width}px`, height: `${props.height}px` }
	})

	const cubeTopSize = computed(() => {
		return { width: `100%`, height: `${props.width / 2}px` }
	})

	const cubeMiddleSize = computed(() => {
		return { width: `100%`, height: `${props.height - props.width / 2}px` }
	})
	
	const cubeMiddleTransform = computed(() => {
		return { transform: `translateY(-${props.width / 2 / 2}px)` }
	})

	const cubeBottomSize = computed(() => {
		return { width: `100%`, height: `${props.width / 2}px` }
	})
	
	const cubeBottomTransform = computed(() => {
		return { transform: `translateY(-${props.width / 2}px)` }
	})
	
	const elementRef = useTemplateRef('element-ref');
	defineExpose({ elementRef });
</script>

<template>
	<div ref="element-ref":style="cubeContainerSize" class="cube-container" >
		<div :style="cubeTopSize" class="cube-top"></div>
		<div :style="{ ...cubeMiddleSize, ...cubeMiddleTransform }" class="cube-middle"></div>
		<div :style="{ ...cubeBottomSize, ...cubeBottomTransform }" class="cube-bottom"></div>
	</div>
</template>

<style lang="css" scoped>
	.cube-container {
		z-index: 10;
	}
	
	.cube-top {
		clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);

		background: linear-gradient(#DDDDDD 20%, #AAAAAA 60%, #888888);
		/* background: linear-gradient(#444444 20%, #666666 60%, #DDDDDD); */

		position: relative;
		z-index: 30;
	}

	.cube-middle {
		background: linear-gradient(#888888 10%, #AAAAAA 40%, #EEEEEE);

		position: relative;
		z-index: 20;
	}

	
	.cube-bottom {
		background-color: #EEEEEE;
		clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);

		position: relative;
		z-index: 10;
	}
</style>