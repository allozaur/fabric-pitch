<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { SvgItem } from "$lib/components/index";

  const assetsPath = "../../../lib/assets/svg/";

  const assets = import.meta.glob("../../../lib/assets/svg/*.svg", {
    query: "?raw",
    import: "default",
    eager: true,
  });

  let mounted = $state(false);

  onMount(() => {
    mounted = true;

    let counter = 0;
    const targetValue = 10;
    const incrementInterval = 200;

    setTimeout(() => {
      const interval = setInterval(() => {
        counter++;

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
      I ❤️ open-source and have contributed <br /> to these incredible projects
    </p>
  {/if}

  <div class="tech-stack">
    {#if mounted}
      <a
        href="https://github.com/sveltejs/kit/pull/12198"
        target="_blank"
        in:fly={{ y: 30, duration: 600, delay: 1000 }}
      >
        <SvgItem name="svelte" --size="5rem" />
      </a>

      <a
        href="https://github.com/storybookjs/storybook/pull/24889"
        target="_blank"
        in:fly={{ y: 30, duration: 600, delay: 1200 }}
      >
        <SvgItem name="storybook" --size="5rem" />
      </a>
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
