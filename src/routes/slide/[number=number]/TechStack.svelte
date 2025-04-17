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
  let numberYears = $state(0);

  onMount(() => {
    mounted = true;

    let counter = 0;
    const targetValue = 4;
    const incrementInterval = 250;

    setTimeout(() => {
      const interval = setInterval(() => {
        counter++;
        numberYears = counter;

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
      I have worked with the following tech stack <br /> for the last <NumberFlow
        value={numberYears}
        transformTiming={{
          duration: 500,
          easing: "cubic-bezier(0.16, 1, 0.3, 1)",
        }}
        spinTiming={{
          duration: 500,
          easing: "cubic-bezier(0.16, 1, 0.3, 1)",
        }}
        opacityTiming={{
          duration: 500,
          easing: "ease-out",
        }}
      /> years
    </p>
  {/if}

  <div class="tech-stack">
    {#if mounted}
      <div in:fly={{ y: 30, duration: 600, delay: 2000 }}>
        <SvgItem {assets} {assetsPath} name="svelte" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2200 }}>
        <SvgItem {assets} {assetsPath} name="vite" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2400 }}>
        <SvgItem {assets} {assetsPath} name="storybook" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2600 }}>
        <SvgItem {assets} {assetsPath} name="postcss" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2800 }}>
        <SvgItem {assets} {assetsPath} name="typescript" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 3000 }}>
        <SvgItem {assets} {assetsPath} name="playwright" --size="3rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 3200 }}>
        <SvgItem {assets} {assetsPath} name="figma" --size="3rem" />
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
