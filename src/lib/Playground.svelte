<script lang="ts">
  import { Render, Runner, Bodies, Composite, Events } from "matter-js";
  import { onMount } from "svelte";
  import { runner } from "./matter/runner";
  import { engine } from "./matter/engine";

  let container: HTMLDivElement;

  onMount(() => {
    const render = Render.create({
      element: container,
      engine,
      options: {
        showDebug: true,
      },
    });

    const boxA = Bodies.rectangle(400, 200, 80, 80);
    const boxB = Bodies.rectangle(450, 50, 80, 80);
    const ground = Bodies.rectangle(400, 620, 810, 60, { isStatic: true });
    const leftWall = Bodies.rectangle(-20, 300, 60, 810, { isStatic: true });
    const rightWall = Bodies.rectangle(820, 300, 60, 810, { isStatic: true });

    Composite.add(engine.world, [boxA, boxB, ground, leftWall, rightWall]);

    Render.run(render);
    Runner.run(runner, engine);
  });
</script>

<div id="#playground" bind:this={container} />
