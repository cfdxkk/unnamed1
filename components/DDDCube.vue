<script setup lang="ts">
  import * as THREE from "three";

  const props = defineProps({
    startEntranceAnimation: {
      type: Boolean,
      require: true,
    }
  })

  const isReady = defineModel('isReady')

  const canvasContainer = useTemplateRef('canvasContainer')
  const width = 300; // 画布宽度
  const height = 300; // 画布高度

  /**
   * 渲染 3D 立方体
   */
  function runder3DCube() {
    if (!canvasContainer.value) return

    // 创建场景
    const scene = new THREE.Scene();

    // 创建相机（透视投影）
    const camera = new THREE.PerspectiveCamera(30, width / height, 0.1, 1000);
    camera.position.z = 10;

    // 创建渲染器
    const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
    renderer.setSize(width, height);
    renderer.setClearColor(0x000000, 0); // 透明背景
    renderer.setPixelRatio(window.devicePixelRatio); // 提高渲染清晰度
    canvasContainer.value.appendChild(renderer.domElement);

    // 创建立方体的几何体
    const geometry = new THREE.BoxGeometry();
    
    // 立方体填充材质（黑色）
    const material = new THREE.MeshBasicMaterial({ color: 0x2f4f4f });

    // 立方体网格对象（黑色填充）
    const cube = new THREE.Mesh(geometry, material);

    // 创建白色边框（使用 EdgesGeometry）
    const edges = new THREE.EdgesGeometry(geometry);
    const lineMaterial = new THREE.LineBasicMaterial({ color: 0xeeeeee });
    const wireframe = new THREE.LineSegments(edges, lineMaterial);

    scene.add(cube);
    scene.add(wireframe);

    // 动画循环
    function animate() {
      requestAnimationFrame(animate);
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      wireframe.rotation.x += 0.01;
      wireframe.rotation.y += 0.01;
      renderer.render(scene, camera);
    }

    animate();

    isReady.value = true;
  }

  onMounted(runder3DCube);
</script>

<template>
  <div ref="canvasContainer" :class="{ 'canvas-container': true, 'entrance': props.startEntranceAnimation }"></div>
</template>

<style lang="css" scoped>
  .canvas-container {
    width: 300px;
    height: 300px;
    opacity: 0;

    position: absolute;
    z-index: 300;
  }

  .entrance {
    animation: entrance_animation 1s ease-in-out 2.2s forwards;
  }

  @keyframes entrance_animation {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
