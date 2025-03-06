<script setup lang="ts">
  const props = defineProps({
    startEntranceAnimation: {
      type: Boolean,
      require: true,
    }
  })

  const router = useRouter()
  const isJumping2ThingsPage = ref(false)
  const isJumping2ThingsPageEnd = ref(false)
  const isShowShadow = ref(true)

  function jump2ThingsPage() {
    const jummpingAnimationDuration = 1000
    isJumping2ThingsPage.value = true

    setTimeout(() => {
      isJumping2ThingsPageEnd.value = true
    }, jummpingAnimationDuration - 200);

    setTimeout(() => {
      router.push('/things')
      isShowShadow.value = false
    }, jummpingAnimationDuration + 600);

    setTimeout(() => {
      isJumping2ThingsPage.value = false
      isJumping2ThingsPageEnd.value = false
      isShowShadow.value = true
    }, jummpingAnimationDuration + 600 + 800);

  }

  const mountedTimes = ref(0)
  const activedTimes = ref(0)
  const isFirstRender = computed(() => activedTimes.value === mountedTimes.value)

  onMounted(() => {
    mountedTimes.value = mountedTimes.value + 1
  })

  onActivated(() => {
    activedTimes.value = activedTimes.value + 1
  })
</script>

<template>
  <div class="main-introduction-contaner">
    <div class="main-introduction-text-contaner">
      <div :class="{ 'title': true, 'entrance-1': props.startEntranceAnimation && isFirstRender }">Things, I like it.</div>
      <div :class="{ 'introduction-text': true, 'entrance-2': props.startEntranceAnimation && isFirstRender }">Here is my website, so I can put whatever I want here.</div>
      <div :class="{ 'introduction-text': true, 'introduction-text-right': true, 'entrance-3': props.startEntranceAnimation && isFirstRender } ">Hi, look at this 3D cube →</div>
      <div :class="{ 'introduction-text': true, 'entrance-4': props.startEntranceAnimation && isFirstRender }">I learned three.js and built it, even though it's useless, I just wanted to put it here.</div>
    </div>
    <div :class="{ 'things-button-container': true, 'entrance-5': props.startEntranceAnimation && isFirstRender }">
      <div class="things-button" @click="jump2ThingsPage">
        Read Blogs →
      </div>
      <div
        class="things-button-animation-bar"
        :style="
          {
            width: `${isJumping2ThingsPage ? 100 : 0}%`,
            left: `${isJumping2ThingsPageEnd ? 100 : 0}%`,
          }
        "
      ></div>
    </div>
    <div
      v-show="isShowShadow"
      class="things-page-shadow"
      :style="
        {
          'box-shadow': `inset ${isJumping2ThingsPageEnd ? -10 : 0}px 0 ${isJumping2ThingsPageEnd ? 40 : 0}px 0px #888888FF`,
          'opacity': isJumping2ThingsPageEnd ? 1 : 0,
        }
      "
    ></div>
  </div>
</template>

<style lang="css" scoped>
  .main-introduction-contaner {
    user-select: none;

    width: 100dvw;
    height: 100dvh;

    overflow: hidden;

    position: absolute;
    top: 0;
    left: 0;

    z-index: 300;
  }

  .main-introduction-text-contaner {
    user-select: none;

    width: 500px;
    overflow: hidden;

    position: absolute;
		top: 30dvh;
		left: 10vw;

    z-index: 300;
  }

  .title {
    font-size: 30px;

    margin: 20px 10px;

    opacity: 1;
  }
  
  .introduction-text {
    margin: 5px 12px;

    opacity: 1;
  }

  .introduction-text-right {
    text-align: right;
  }

  .things-button-container {
    width: 90dvw;
    height: 30px;

    overflow: hidden;

    position: absolute;
		top: 45dvh;
		left: 10vw;

    margin: 100px 0 0 12px;
  }

  .things-button {
    width: fit-content;

    cursor: pointer;
  }

  .things-button-animation-bar {
    width: 100%;
    height: 5px;

    background-color: #888888;

    position: absolute;
    top: 25px;

    transition: width 1s ease-in-out, left 0.8s ease-in-out;
  }

  .things-page-shadow {
    pointer-events: none;
    width: 100%;
    height: 110dvh;

    transition: box-shadow 0.6s, opacity 0.3s;

    position: absolute;
    top: -5vh;
    left: 0;
  }

  .entrance-1 {
    animation: entrance_animation 1s ease-in-out 0s both;
  }

  .entrance-2 {
    animation: entrance_animation 0.6s ease-in-out 1s both;
  }

  .entrance-3 {
    animation: entrance_animation 0.6s ease-in-out 1.6s both;
  }

  .entrance-4 {
    animation: entrance_animation 0.6s ease-in-out 2.8s both;
  }

  .entrance-5 {
    animation: entrance_animation 0.6s ease-in-out 3.4s both;
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
