<script setup lang="ts">
	const props = withDefaults(defineProps<{
    isSlow?: boolean;
    showBackground?: boolean;
    loadingBarWidth?: number;
    loadingBarHeigth?: number;
  }>(), {
    isSlow: true,
    showBackground: true,
    loadingBarWidth: 200,
    loadingBarHeigth: 3,
  })

  const loadingBarItem = useTemplateRef('loading-bar-item')
  
  const computedLoadingBarSize = computed(() => {
    return {
      width: `${props.loadingBarWidth}px`,
      height: `${props.loadingBarHeigth}px`,
      'border-radius': `${props.loadingBarHeigth}px ${props.loadingBarHeigth}px`,
    }
  })

  const computedLoadingBarItemBorderRadius = computed(() => {
    return {
      'border-radius': `${props.loadingBarHeigth}px ${props.loadingBarHeigth}px`,
    }
  })

  /**
   * 根据传入的参数判断是否启动慢速动画
   * @param isSlow 是否为慢速动画
   */
  function changeAnimationNextSpeed(isSlow: boolean) {
    const loadingBarItemElement = loadingBarItem.value
    if (!loadingBarItemElement) return
    const [loadingBarItemElementAnimation] = loadingBarItemElement.getAnimations();

    if (isSlow)
      loadingBarItemElementAnimation.playbackRate = 1;
    else
      loadingBarItemElementAnimation.playbackRate = 2;
  }

  watch(() => props.isSlow, isSlow => changeAnimationNextSpeed(isSlow))
</script>

<template>
  <div :style="computedLoadingBarSize" :class="{ 'loading-bar-contaner': true, 'loading-bar-background-active' :showBackground }">
    <div ref="loading-bar-item" :style="computedLoadingBarItemBorderRadius" class="loading-bar-item"></div>
  </div>
</template>

<style lang="css" scoped>
  .loading-bar-contaner {
    width: 200px;
    height: 3px;

    border-radius: 3px 3px;
    overflow: hidden;

    position: absolute;
    z-index: 999;
  }

  .loading-bar-background-active {
    background-color: #DDDDDD;
  }

  .loading-bar-item {
    height: 100%;
    width: 30%;

    background-color: #888888;

    position: relative;

    animation: loading_bar_item_animation 0.5s ease-in-out infinite alternate;
  }

  @keyframes loading_bar_item_animation {
    from {
      left: -25%;
    }
    to {
      left: 95%;
    }
  }
</style>
