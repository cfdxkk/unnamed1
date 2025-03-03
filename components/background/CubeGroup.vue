<script setup lang="ts">

</script>

<template>
	<div class="cube-group-container">
		<BackgroundCube :width="200" :height="2000" class="cube-1" />
		<BackgroundCube :width="200" :height="2000" class="cube-2" />
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

    right: 20vw;
    top: -20vh;

    transform: rotate(-45deg) translate(300px, 300px);
    animation: move_cube_1 8s ease-in-out forwards;
  }

  @keyframes move_cube_1 {
    from {
      transform: rotate(-45deg) translate(300px, 300px);
    }
    to {
      transform: rotate(-45deg) translate(300px, 200px);
    }
  }

  .cube-2 {
    position: absolute;

    right: 20vw;
    top: 5vh;

    transform: rotate(-45deg) translate(300px, 320px);
    animation: move_cube_2 6s ease-out 0.2s forwards;
  }

  @keyframes move_cube_2 {
    from {
      transform: rotate(-45deg) translate(300px, 320px);
    }
    to {
      transform: rotate(-45deg) translate(300px, 200px);
    }
  }

</style>