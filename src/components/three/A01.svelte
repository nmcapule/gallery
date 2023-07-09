<script>
  import { onMount } from "svelte";
  import * as THREE from "three";

  let container;

  onMount(async () => {
    const width = container.offsetWidth;
    const height = container.offsetHeight;

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      width / height,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(width, height);
    container.appendChild(renderer.domElement);

    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    function animate() {
      requestAnimationFrame(animate);

      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;

      renderer.render(scene, camera);
    }

    animate();
  });
</script>

<div class="renderer-container" bind:this={container} />

<style lang="scss">
  .renderer-container {
    width: 68ch;
    height: 68ch;
    border-radius: 6px;
  }
</style>
