<script>
  import * as THREE from "three";
  import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";
  import { onMount } from "svelte";
  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import gsap from "gsap";
  import ScrollTrigger from "gsap/ScrollTrigger";

  let scene;
  let camera;
  let renderer;
  let container;
  let mesh;

  onMount(() => {
    const container = document.getElementById("3d"); // Get the 3d div

    const scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(
      25,
      window.innerWidth / window.innerHeight,
      1,
      20000
    );
    camera.position.z = 5000; // Change this value to zoom out further

    const light = new THREE.AmbientLight(0xfffffff);
    scene.add(light);
    const renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setClearColor(0x000000, 0);
    renderer.setSize(window.innerWidth, window.innerHeight);

    container.appendChild(renderer.domElement);
    const loader = new GLTFLoader();
    let model;

    // Load the GLB model
    loader.load("pluto.glb", (gltf) => {
      model = gltf.scene;
      scene.add(model);
    });

    const animate = () => {
      requestAnimationFrame(animate);

      // Rotate the loaded model
      if (model) {
        model.rotation.y += 0.004;
      }

      renderer.render(scene, camera);
    };

    animate();
    gsap.registerPlugin(ScrollTrigger);
    gsap.set(".labelg", {
      opacity: 0,

      y: -12,
    });
    gsap.to(".labelg", {
      opacity: 1,
      duration: 2,
      y: 0,
      scrub: true,
      scrollTrigger: ".labelg",
    });
  });
</script>

<main>
  <div class="column-container">
    <h1 class="labelg">Pluto</h1>
    <div style="max-width: 100%; overflow: hidden;" class="d3" id="3d" />
    <p class="desc2">
      Pluto Is the Most popular Dwarf planet, as it received a demotion from the
      oficial title of planet in 2006.
    </p>
  </div>
</main>
