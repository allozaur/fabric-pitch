<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { SvgItem } from "$lib/components/index";

  let mounted = $state(false);

  onMount(() => {
    mounted = true;
  });
</script>

<main>
  {#if mounted}
    <p in:fly={{ y: 50, duration: 800, delay: 300 }}>
      This is my current go-to tech stack for UI engineering
    </p>
  {/if}

  <div class="tech-stack">
    {#if mounted}
      <div in:fly={{ y: 30, duration: 600, delay: 1000 }}>
        <SvgItem name="svelte" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 1250 }}>
        <SvgItem name="vite" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 1500 }}>
        <SvgItem name="typescript" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 1750 }}>
        <SvgItem name="postcss" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2000 }}>
        <SvgItem name="storybook" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2250 }}>
        <SvgItem name="playwright" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2500 }}>
        <SvgItem name="vitest" --size="4rem" />
      </div>
      <div in:fly={{ y: 30, duration: 600, delay: 2750 }}>
        <SvgItem name="figma" --size="4rem" />
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
    gap: 4rem;
    padding-block: 2rem;
  }
</style>
