<script setup lang="ts">
  const props = defineProps({
    startEntranceAnimation: {
      type: Boolean,
      require: true,
    }
  })

  const router = useRouter()

  function jump2ThingsPage() {
    router.push('/things')
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
    <div :class="{ 'title': true, 'entrance-1': props.startEntranceAnimation && isFirstRender }">Things, I like it.</div>
    <div :class="{ 'introduction-text': true, 'entrance-2': props.startEntranceAnimation && isFirstRender }">Here is my website, so I can put whatever I want here.</div>
    <div :class="{ 'introduction-text': true, 'introduction-text-right': true, 'entrance-3': props.startEntranceAnimation && isFirstRender } ">Hi, look at this 3D cube →</div>
    <div :class="{ 'introduction-text': true, 'entrance-4': props.startEntranceAnimation && isFirstRender }">I learned three.js and built it, even though it's useless, I just wanted to put it here.</div>
    <div 
      :class="{ 'things-button': true, 'entrance-5': props.startEntranceAnimation && isFirstRender }" 
      @click="jump2ThingsPage"
    >
      Things
    </div>
  </div>
</template>

<style lang="css" scoped>
  .main-introduction-contaner {
    user-select: none;
    
    width: 500px;
    overflow: hidden;

    position: absolute;

    z-index: 300;
  }

  .title {
    font-size: 30px;

    padding: 20px 10px;

    opacity: 1;
  }
  
  .introduction-text {
    padding: 5px 12px;

    opacity: 1;
  }

  .introduction-text-right {
    text-align: right;
  }

  .things-button {
    padding: 100px 0 0 12px;
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
