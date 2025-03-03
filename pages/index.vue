<script setup lang="ts">

</script>

<template>
	<div>
		<div class="blur"></div>
		<BackgroundCubeGroup />
	</div>
</template>

<style lang="css" scoped>
	.blur {
		height: 100dvh;
		width: 100dvw;

		background-color: #EEEEEE00;
		backdrop-filter: blur(2px);
    animation: blur_animation 8s ease-in-out 2s forwards;

		position: absolute;
		z-index: 999;
	}

	@keyframes blur_animation {
		from {
      background-color: #EEEEEE00;
			backdrop-filter: blur(2px);
		}
		to {
			background-color: #EEEEEECC;
			backdrop-filter: blur(6px);
		}
	}
</style>