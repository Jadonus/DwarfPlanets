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
  import Rellax from "rellax";

  onMount(() => {
    var rellax = new Rellax(".rellax", { center: true });
    const scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(
      25,
      window.innerWidth / window.innerHeight,
      1,
      20000
    );

    camera.position.z = 30; // Change this value to zoom out further

    const light = new THREE.AmbientLight(0xfffffff);
    scene.add(light);
    const renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setClearColor(0x000000, 0);
    renderer.setSize(window.innerWidth, window.innerHeight);
    const container = document.getElementById("3d"); // Get the 3d div

    const controls = new OrbitControls(camera, renderer.domElement);

    controls.update();

    container.appendChild(renderer.domElement);
    const loader = new GLTFLoader();
    let model;

    // Load the GLB model
    loader.load("voyager.glb", (gltf) => {
      model = gltf.scene;
      scene.add(model);
    });

    const animate = () => {
      requestAnimationFrame(animate);

      // Rotate the loaded model
      if (model) {
        controls.enableZoom = false; // No zooming allowed
        controls.enablePan = false;

        controls.update();
      }

      renderer.render(scene, camera);
    };

    animate();
    gsap.registerPlugin(ScrollTrigger);
    gsap.set(".label", {
      opacity: 0,

      y: -14,
    });
    gsap.to(".label", {
      opacity: 1,
      duration: 2,
      y: -10,
      scrub: true,
      scrollTrigger: ".label",
    });
  });
</script>

<main class="im">
  <h1 class="label6">Voyager</h1>
  <div class="d3" style="max-width: 100%; overflow: hidden;" id="3d" />

  <p class="desc6">
    This is voyager. This probe was launched in 1977 on a one way mission. It
    went to explore planets like these in the kuiper belt.
  </p>
</main>
