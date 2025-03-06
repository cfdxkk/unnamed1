<script setup lang="ts">
  const route = useRoute()
  
  const pos = ref(route.path === '/things' ? 50 : 20) // 初始位置根据路由决定

  function moveLeft() {
    // 如果已经在距右侧 50dvw，则不执行动画
    if (pos.value === 50) return
    pos.value = 50
  }

  function moveRight() {
    // 如果已经在距右侧 20dvw，则不执行动画
    if (pos.value === 20) return
    pos.value = 20
  }

  function checkAndTriggedAnimation(routePath: string) {
    if (routePath === '/')
      moveRight();
    else if (routePath === '/things')
      moveLeft();
  }

  watch(() => route.path, checkAndTriggedAnimation)
</script>

<template>
	<div class="cube-group-container">
		<BackgroundCube :width="200" :height="2000" class="cube-1" :style="{ right: `${pos}dvw`}" />
		<BackgroundCube :width="200" :height="2000" class="cube-2" :style="{ right: `${pos}dvw`}"  />
	</div>
</template>

<style lang="css" scoped>
	.cube-group-container {
    position: relative;
    top: 0;
    left: 0;

		height: 100dvh;
		width: 100dvw;

		overflow: hidden;
	}

  .cube-1 {
    position: absolute;

    top: -20dvh;

    animation: move_cube_1 6s ease-in-out both;

    transition: right 1.5s ease-in-out;
  }

  @keyframes move_cube_1 {
    from {
      transform: rotate(-45deg) translate(300px, 300px);
    }
    to {
      transform: rotate(-45deg) translate(300px, 260px);
    }
  }

  .cube-2 {
    position: absolute;

    top: 5dvh;

    animation: move_cube_2 5s ease-in-out 0.2s both;

    transition: right 1.5s ease-in-out;
  }

  @keyframes move_cube_2 {
    from {
      transform: rotate(-45deg) translate(300px, 320px);
    }
    to {
      transform: rotate(-45deg) translate(300px, 250px);
    }
  }

</style>