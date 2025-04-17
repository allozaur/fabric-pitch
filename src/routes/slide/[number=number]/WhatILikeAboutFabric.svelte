<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { SvgItem } from "$lib/components/index";

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
      3 things I really like about <SvgItem name="fabric" --size="1.75rem" />'s
      ecosystem
    </p>
  {/if}

  <ol class="reasons">
    {#if mounted}
      <li in:fly={{ y: 30, duration: 600, delay: 1000 }}>
        It's <strong>decentralized</strong> as all of Web3 should be
      </li>

      <li in:fly={{ y: 30, duration: 600, delay: 2000 }}>
        It's a <strong>well-thought product suite</strong>
      </li>

      <li in:fly={{ y: 30, duration: 600, delay: 3000 }}>
        <strong>High quality design</strong> is one of the foundations, not a nuance
      </li>
    {/if}
  </ol>
</main>

<style>
  main {
    height: 100vh;
    display: grid;
    place-content: center;
  }

  ol {
    padding: 1.375rem;
    font-size: 1.25rem;
  }

  p {
    font-size: 2rem;
    line-height: 1.5;
    text-align: center;
  }

  p :global(svg) {
    translate: 0 0.125rem;
    margin-inline: 0.275rem 0.125rem;
  }

  strong {
    font-weight: 800;
    background: var(--bg-surface-1);
    padding: 0.375rem;
  }

  .reasons {
    display: grid;
    align-items: center;
    gap: 4rem;
    padding-block: 2rem;
  }
</style>
