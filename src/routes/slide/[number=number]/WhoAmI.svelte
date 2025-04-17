<script>
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import NumberFlow from "@number-flow/svelte";

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
      I am an UI/UX Designer & Software Engineer <br /> with <NumberFlow
        value={yearsExperience}
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
      /> years of experience in creating digital products
    </p>
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
