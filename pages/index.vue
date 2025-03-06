<script setup lang="ts">
	const isSlow = ref(true)
	const is3DCubeReady = ref(false)
	const isBackgroundAnimationFinished = ref(false)

	const isShowIntroduction = computed({
		get: () => isBackgroundAnimationFinished.value && is3DCubeReady.value,
		set: value => is3DCubeReady.value = value,
	})

	onMounted(() => {
		setInterval(() => {
			isSlow.value = !isSlow.value
		}, 3000);

		setTimeout(() => {
			isBackgroundAnimationFinished.value = true
		}, 6000)

		setTimeout(() => {
			isShowIntroduction.value = true
		}, 6000)
	})

	definePageMeta({
		keepalive: true,
    pageTransition: {
      name: 'home',
    },
	});
</script>

<template>
	<div class="main">
		<MainIntroduction v-show="isShowIntroduction" :startEntranceAnimation="isShowIntroduction"/>
		<DDDCube v-show="isShowIntroduction" class="ddd-cube" :startEntranceAnimation="isShowIntroduction" v-model:isReady="is3DCubeReady"/>
		<LoadingBar v-if="!isShowIntroduction" class="loading-bar" :isSlow="isSlow" :loadingBarWidth="250" :loadingBarHeigth="4" :showBackground="false"/>
	</div>
</template>

<style lang="css" scoped>
	.main {
		width: 100dvw;
		height: 100dvh;

		overflow: hidden;

		position: absolute;
		top: 0;
		left: 0;
		z-index: 300;
	}

	.ddd-cube {
		top: 27dvh;
		left: calc(10dvw + 450px);
	}

	.loading-bar {
		top: 40dvh;
		left: 20dvw;
	}
</style>