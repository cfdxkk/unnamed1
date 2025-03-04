<script setup lang="ts">
  const props = defineProps({
    startEntranceAnimation: {
      type: Boolean,
      require: true,
    }
  })
</script>

<template>
  <div class="main-introduction-contaner">
    <div :class="{ 'title': true, 'entrance-1': props.startEntranceAnimation }">Things, I like it.</div>
    <div :class="{ 'introduction-text': true, 'entrance-2': props.startEntranceAnimation }">Here is my website, so I can put whatever I want here.</div>
    <div :class="{ 'introduction-text': true, 'introduction-text-right': true, 'entrance-3': props.startEntranceAnimation } ">Hi, look at this 3D cube →</div>
    <div :class="{ 'introduction-text': true, 'entrance-4': props.startEntranceAnimation }">I learned three.js and built it, even though it's useless, I just wanted to put it here.</div>
  </div>
</template>

<style lang="css" scoped>
  .main-introduction-contaner {
    pointer-events: none;

    width: 500px;
    overflow: hidden;

    position: absolute;

    z-index: 300;
  }

  .title {
    font-size: 30px;

    padding: 20px 10px;

    transform: translate(-5px, -10px);
    opacity: 0;
  }
  
  .introduction-text {
    padding: 5px 12px;

    transform: translate(-5px, -10px);
    opacity: 0;
  }

  .introduction-text-right {
    text-align: right;
  }

  .entrance-1 {
    animation: entrance_animation 1s ease-in-out 0s forwards;
  }

  .entrance-2 {
    animation: entrance_animation 0.6s ease-in-out 1s forwards;
  }

  .entrance-3 {
    animation: entrance_animation 0.6s ease-in-out 1.6s forwards;
  }

  .entrance-4 {
    animation: entrance_animation 0.6s ease-in-out 3.2s forwards;
  }

  @keyframes entrance_animation {
    from {
      transform: translate(-5px, -10px);
      opacity: 0;
    }
    to {
      transform: translate(0, 0);
      opacity: 1;
    }
  }
</style>
