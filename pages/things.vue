<script setup lang="ts">
  definePageMeta({
    pageTransition: {
      name: 'things',
    },
  })
</script>

<template>
  <div class="things-container">
    aaaaaaaaaaaa
    <NuxtLink to="/" style="position: absolute; z-index: 300; top: 200px; left: 200px;">Back</NuxtLink>
  </div>
</template>

<style lang="css" scoped>
  .things-container {
    width: 100dvw;
    height: 100dvh;

    color: #FFFFFF;

    background-color: #222222AA;

    position: absolute;
    z-index: 300;
    top: 0;
    left: 0;
  }
</style>
