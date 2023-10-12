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
    camera.position.z = 5000; // Change this value to zoom out further

    const light = new THREE.AmbientLight(0xfffffff);
    scene.add(light);
    const renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setClearColor(0x000000, 0);
    renderer.setSize(window.innerWidth, window.innerHeight);
    const container = document.getElementById("3d"); // Get the 3d div

    container.appendChild(renderer.domElement);
    const loader = new GLTFLoader();
    let model;

    // Load the GLB model
    loader.load("makemake.glb", (gltf) => {
      model = gltf.scene;
      scene.add(model);
    });

    const animate = () => {
      requestAnimationFrame(animate);

      // Rotate the loaded model
      if (model) {
        model.rotation.y += 0.003;
      }

      renderer.render(scene, camera);
    };

    animate();
    gsap.registerPlugin(ScrollTrigger);
    gsap.set(".label", {
      opacity: 0,

      y: -14,
    });
    gsap.to(".desc4", {
      opacity: 1,
      duration: 2,
      y: -10,
      scrub: true,
      scrollTrigger: ".desc4",
    });
  });
</script>

<main class="im">
  <h1 class="label4">Makemake</h1>
  <div class="" style="max-width: 100%; overflow: hidden;" id="3d" />

  <p class="desc4">
    Makemake is about as big as pluto, and is covered in ice, making it very
    bright for astronomers.
  </p>
</main>
