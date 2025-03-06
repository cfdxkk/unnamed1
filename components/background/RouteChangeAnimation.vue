<script setup lang="ts">
  const route = useRoute()
  
  const pos = ref(route.path === '/things' ? 0 : -100) // 初始位置根据路由决定
  const duration = ref(route.path === '/things' ? 0.9 : 0.7) // 动画时长根据路由决定


  // 计算样式：包含 left 值和 transition 时间
  const animationContainerStyle = computed(() => ({
    right: pos.value + 'dvw',
    transition: `right ${duration.value}s ease-in-out`
  }))

  function moveLeft() {
    // 如果已经在距右侧 0dvw，则不执行动画
    if (pos.value === 0) return
    duration.value = 0.7  // 向左移动时 1s
    pos.value = 0
  }

  function moveRight() {
    // 如果已经在距右侧 -100dvw，则不执行动画
    if (pos.value === -100) return
    duration.value = 0.9  // 向右移动时 0.5s
    pos.value = -100
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
  <div class="route-change-animation-container" :style="animationContainerStyle"></div>
</template>

<style lang="css" scoped>
  .route-change-animation-container {
    height: 100dvh;
    width: 100dvw;

    background-color: #AAAAAA70;

    position: absolute;
    top: 0;

    z-index: 250;
  }
</style>
