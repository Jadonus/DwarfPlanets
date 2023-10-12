<script lang="ts">
  import "./app.css";
  import Ceres from "./lib/Ceres.svelte";
  import Haumea from "./lib/Haumea.svelte";
  import Makemake from "./lib/Makemake.svelte";
  import Eris from "./lib/Eris.svelte";
  import Pluto from "./lib/Pluto.svelte";
  import Voyager from "./lib/Voyager.svelte";
  import Sep from "./lib/Sep.svelte";
  import Footer from "./lib/Footer.svelte";
  import Message from "./lib/Message.svelte";
</script>

<main>
  <div class="img">
    <div class="center">
      <h1>Get to know the dwarf planets</h1>
    </div>
  </div>
  <div class="column-container">
    <Ceres />
    <Sep />
    <Pluto />
    <Sep />
    <Haumea />
    <Sep />
    <Makemake />
    <Sep />
    <Eris />
    <Sep />
    <Voyager />
    <Message />
    <Footer />
  </div>
</main>
