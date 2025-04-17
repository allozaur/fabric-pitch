<script>
  import memeBackground from "$lib/assets/png/meme-background.png?enhanced";
  import { onMount } from "svelte";
  import { fly, scale } from "svelte/transition";

  let mounted = $state(false);

  onMount(() => {
    mounted = true;
  });
</script>

<main>
  {#if mounted}
    <p in:fly={{ y: 50, duration: 800, delay: 300 }}>
      How I see our cooperation
    </p>

    <div class="meme" in:scale={{ duration: 800, delay: 1000 }}>
      <enhanced:img
        src={memeBackground}
        height="560"
        alt="Teamwork makes dreams work"
      ></enhanced:img>
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

  p {
    font-size: 2rem;
    line-height: 1.5;
    text-align: center;
  }
</style>
