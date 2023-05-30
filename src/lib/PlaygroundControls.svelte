<script lang="ts">
  import { Bodies, Composite, Events } from "matter-js";
  import { engine } from "./matter/engine";
  import { onDestroy } from "svelte";

  function createRectangle() {
    const rect = Bodies.rectangle(
      400,
      200,
      Math.max(Math.random() * 40, 5),
      Math.max(Math.random() * 40, 5)
    );

    Composite.add(engine.world, [rect]);
  }

  function createCircle() {
    const circle = Bodies.circle(400, 200, Math.max(Math.random() * 20, 5));

    Composite.add(engine.world, [circle]);
  }

  function clearWorld() {
    Composite.clear(engine.world, true);
  }

  const interval = setInterval(() => {
    createCircle();
  }, 50);
  onDestroy(() => {
    clearInterval(interval);
  });
</script>

<div class="overlay">
  <div class="spawner">
    <h2 class="spawner__title">Spawner</h2>
    <div class="spawner__buttons">
      <button on:click={createRectangle}>Rectangle</button>
      <button on:click={createCircle}>Circle</button>
      <button on:click={clearWorld}>Clear</button>
    </div>
  </div>
</div>

<style>
  .overlay {
    background: #00000033;
    position: absolute;
    right: 0;
    top: 0;
    margin: 0.5em;
    padding: 1em;
    border-radius: 0.75em;
  }

  .spawner {
    display: flex;
    flex-direction: column;
  }

  .spawner__title {
    margin: 0;
    margin-bottom: 1em;
  }

  .spawner__buttons {
    display: flex;
    flex-direction: column;
    gap: 0.5em;
  }
</style>
