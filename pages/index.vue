<script setup lang="ts">
	const isSlow = ref(false)

	// REMOVE: Test loading bar speed.
	onMounted(() => {
		setInterval(() => {
		isSlow.value = !isSlow.value
	}, 5000);
	})
</script>

<template>
	<div>
		<LoadingBar style="top: 300px; left: 400px;" :isSlow :loadingBarWidth="250" :loadingBarHeigth="4" :showBackground="false"/>
		<BackgroundBlur />
		<BackgroundCubeGroup />
	</div>
</template>

<style lang="css" scoped>

</style>