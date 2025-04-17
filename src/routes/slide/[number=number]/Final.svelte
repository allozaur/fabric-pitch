<script>
  import memeBackground from "$lib/assets/png/meme-background.png?enhanced";
  import Button from "$lib/components/Button/Button.svelte";
  import SvgItem from "$lib/components/SvgItem/SvgItem.svelte";
  import { onMount } from "svelte";
  import { fly, scale } from "svelte/transition";

  let mounted = $state(false);

  onMount(() => {
    mounted = true;
  });
</script>

<main>
  {#if mounted}
    <h2 in:fly={{ y: 50, duration: 800 }}>Thank you!</h2>

    <p in:fly={{ y: 50, duration: 800, delay: 500 }}>
      I am looking forward to joining <SvgItem name="fabric" --size="1.75rem" />
      team!
    </p>

    <div class="cta" in:fly={{ y: 50, duration: 800, delay: 1500 }}>
      <Button href="mailto:aleksander.grygier@gmail.com">
        👉 Click to hire 👈
      </Button>
    </div>
  {/if}
</main>

<style>
  main {
    height: 100vh;
    display: grid;
    place-content: center;
    place-items: center;
  }

  h2 {
    font-size: 3rem;
    line-height: 1.5;
    text-align: center;
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

  .cta {
    margin-top: 4rem;
  }
</style>
