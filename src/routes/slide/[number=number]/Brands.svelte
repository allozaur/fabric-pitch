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
      In recent years I've been working on
    </p>
  {/if}

  <div class="brands">
    {#if mounted}
      <a
        href="https://concepts.app/"
        target="_blank"
        style="margin-left: -0.25rem"
        in:fly={{ y: 30, duration: 600, delay: 1000 }}
      >
        <SvgItem name="concepts" --size="2.875rem" />
      </a>

      <a
        href="https://tradingstrategy.ai"
        target="_blank"
        in:fly={{ y: 30, duration: 600, delay: 1250 }}
      >
        <SvgItem name="tradingstrategy-ai" --size="2.75rem" />
      </a>

      <a
        href="https://www.resider.pl/en"
        target="_blank"
        in:fly={{ y: 30, duration: 600, delay: 1500 }}
      >
        <SvgItem name="resider" --size="2.5rem" />
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

  a {
    display: inline-flex;
    color: var(--c-text);
    text-decoration: none;
  }

  .brands {
    display: flex;
    align-items: center;
    gap: 4rem;
    padding-block: 2rem;
  }
</style>
