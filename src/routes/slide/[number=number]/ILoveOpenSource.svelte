<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { SvgItem } from "$lib/components/index";
  import NumberFlow from "@number-flow/svelte";

  const assetsPath = "../../../lib/assets/svg/";

  const assets = import.meta.glob("../../../lib/assets/svg/*.svg", {
    query: "?raw",
    import: "default",
    eager: true,
  });

  let mounted = $state(false);
  let yearsExperience = $state(0);

  onMount(() => {
    mounted = true;

    let counter = 0;
    const targetValue = 10;
    const incrementInterval = 200;

    setTimeout(() => {
      const interval = setInterval(() => {
        counter++;
        yearsExperience = counter;

        if (counter >= targetValue) {
          clearInterval(interval);
        }
      }, incrementInterval);
    }, 250);
  });
</script>

<main>
  {#if mounted}
    <p in:fly={{ y: 50, duration: 800, delay: 300 }}>
      I ❤️ open-source and have contributed to these incredible projects
    </p>
  {/if}

  <div class="tech-stack">
    {#if mounted}
      <div in:fly={{ y: 30, duration: 600, delay: 1000 }}>
        <SvgItem {assets} {assetsPath} name="svelte" --size="5rem" />
      </div>

      <div in:fly={{ y: 30, duration: 600, delay: 1200 }}>
        <SvgItem {assets} {assetsPath} name="storybook" --size="5rem" />
      </div>
    {/if}
  </div>
</main>

<style>
  main {
    height: 100vh;
    display: grid;
    place-content: center;
    place-items: center;
  }

  p {
    font-size: 2rem;
    line-height: 1.5;
    text-align: center;
  }

  .tech-stack {
    display: flex;
    gap: 3rem;
    padding-block: 2rem;
  }
</style>
