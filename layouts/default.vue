<template>
  <div class="main-page">
    <slot />
    <BackgroundBlur />
		<BackgroundCubeGroup />
  </div>
</template>

<style lang="css" scoped>
  .main-page {
    width: 100dvw;
    height: 100dvh;

    overflow: hidden;
    
    margin: 0;
    padding: 0;

    position: absolute;
    top: 0;
    left: 0;
  }
</style>
