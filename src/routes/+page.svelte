<script lang="ts">
  import profilePicture from "$lib/assets/png/profile-pic.png?enhanced";
  import { fly } from "svelte/transition";
  import { elasticOut } from "svelte/easing";
  import { Button } from "$lib/components/index.js";
  import { onMount } from "svelte";
  import { goto } from "$app/navigation";

  let peekState = $state("hidden");
  let showGreeting = $state(false);
  let showFinalImage = $state(false);
  let showName = $state(false);
  let typewriterComplete = $state(false);

  function gentleElasticOut(t: number) {
    const amplitude = 0.25;
    const period = 0.3;

    return (
      amplitude *
        Math.pow(2, -10 * t) *
        Math.sin(((t - period / 4) * (2 * Math.PI)) / period) +
      1
    );
  }

  function goToNextPage() {
    if (showFinalImage) {
      goto("/slide/1");
    }
  }

  function onTypewriterComplete() {
    typewriterComplete = true;
    setTimeout(() => {
      showName = true;
      showFinalImage = true;
    }, 500);
  }

  function spin(
    node: HTMLElement,
    { duration, delay }: { duration: number; delay: number }
  ) {
    return {
      duration,
      delay,
      css: (t: number, u: any) => {
        const eased = elasticOut(t);
        return `
          transform: scale(${eased}) rotate(${eased * 720}deg);
        `;
      },
    };
  }

  function startPeekSequence() {
    peekState = "peekBottom";

    setTimeout(() => {
      peekState = "hidden";

      setTimeout(() => {
        showGreeting = true;
      }, 2000);
    }, 2000);
  }

  onMount(() => {
    startPeekSequence();
  });
</script>

<svelte:head>
  <style>
    body {
      overflow: hidden;
    }
  </style>
</svelte:head>

<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
<!-- svelte-ignore a11y_click_events_have_key_events -->
<main class:image-active={showFinalImage} onclick={goToNextPage}>
  {#if showGreeting}
    <div class="content-wrapper" class:slide-up={showFinalImage}>
      <h1 class="heading">
        <span
          class="typewriter"
          class:completed={typewriterComplete}
          onanimationend={onTypewriterComplete}
          >Hi, I'm
        </span>
        {#if showName}
          <strong class="name">Alek</strong>
        {/if}
      </h1>
    </div>
  {/if}

  {#if peekState === "peekBottom"}
    <div
      class="image-wrapper peek-bottom"
      in:fly|local={{
        y: 200,
        delay: 500,
        duration: 1500,
        easing: (t) => t * t * t,
      }}
      out:fly|local={{ y: 200, delay: 1000, duration: 1000 }}
    >
      <enhanced:img src={profilePicture} height="250"></enhanced:img>
    </div>
  {/if}

  {#if showFinalImage}
    <div
      class="final-image"
      in:fly={{ y: 300, duration: 500, easing: gentleElasticOut }}
    >
      <enhanced:img src={profilePicture} height="250"></enhanced:img>
    </div>
  {/if}

  {#if showFinalImage}
    <div class="start-button-wrapper" in:spin={{ duration: 2000, delay: 500 }}>
      <Button href="/slide/1">Start 🚀</Button>
    </div>
  {/if}
</main>

<style>
  @keyframes bumpUp {
    0% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-40px);
    }
    70% {
      transform: translateY(-25px);
    }
    100% {
      transform: translateY(-30px);
    }
  }

  @keyframes typing {
    0% {
      width: 0;
      border-right: 2px solid #222;
    }
    99% {
      border-right: 2px solid #222;
    }
    100% {
      width: 100%;
      border-right: 2px solid transparent;
    }
  }

  @keyframes nameBumpUp {
    0% {
      transform: translateY(20px);
      opacity: 0;
    }
    10% {
      transform: translateY(-24px);
      opacity: 1;
    }
    50% {
      transform: translateY(0px);
    }
    70% {
      transform: translateY(-6px);
    }
    85% {
      transform: translateY(-2px);
    }
    100% {
      transform: translateY(0);
      opacity: 1;
    }
  }

  main {
    display: grid;
    height: 100vh;
    place-items: center;
    place-content: center;
    position: relative;
    overflow: hidden;
  }

  .content-wrapper {
    transition: none;
    will-change: transform;
    z-index: 1;
    margin-bottom: 1rem;

    h1 {
      margin: 0;
    }
  }

  .content-wrapper.slide-up {
    animation: bumpUp 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
  }

  .heading {
    font-weight: 400;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 2.5rem;
  }

  .typewriter {
    position: relative;
    width: fit-content;
    border-right: 2px solid transparent;
    white-space: nowrap;
    overflow: hidden;
    animation: typing 0.75s steps(8, end) forwards;
  }

  .typewriter.completed {
    border-right: 2px solid transparent;
  }

  .name {
    display: inline-block;
    font-weight: 700;
    background: var(--bg-surface-1);
    padding: 0.25rem 0.5rem;
    margin-left: 0.25rem;
    animation: nameBumpUp 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
  }

  .image-wrapper {
    position: relative;
    transform-style: preserve-3d;
    backface-visibility: hidden;
    will-change: transform;
  }

  .peek-bottom {
    position: absolute;
    bottom: -125px;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
    width: fit-content;
  }

  .final-image {
    position: relative;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
    width: fit-content;
    z-index: 0;
  }

  .start-button-wrapper {
    display: flex;
    position: relative;
    transform-origin: center center;
    margin-top: 3rem;
  }
</style>
