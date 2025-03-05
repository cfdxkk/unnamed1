<template>
  <div>
    <NuxtLayout>
      <NuxtPage keepalive/>
    </NuxtLayout>
  </div>
</template>

<style lang="css">
  body {
    margin: 0;
    padding: 0;

    background-color: white;
  }

  .things-enter-active{
    transition: all 0.8s ease-in-out;
  }
  .things-leave-active {
    transition: all 0.6s ease-in-out;
  }
  .things-enter-from,
  .things-leave-to {
    opacity: 0.8;
    transform: translate(100dvw, 0);
  }

  .home-enter-active{
    transition: all 0.8s ease-in-out;
  }
  .home-leave-active {
    transition: all 0.6s ease-in-out;
  }
  .home-enter-from,
  .home-leave-to {
    opacity: 0.5;
    transform: translate(-100dvw, 0);
  }
</style>
