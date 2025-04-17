<script lang="ts">
  import profilePicture from "$lib/assets/png/profile-pic.png?enhanced";
  import { fly, fade } from "svelte/transition";
  import { Button } from "$lib/components/index.js";

  let hasStarted = $state(false);
  let peekState = $state("hidden");
  let typewriterComplete = $state(false);
  let showName = $state(false);
  let showGreeting = $state(false);
  let showFinalImage = $state(false);
  let showNextButton = $state(false);

  function gentleElasticOut(t: number) {
    const amplitude = 0.5;
    const period = 0.3;

    return (
      amplitude *
        Math.pow(2, -10 * t) *
        Math.sin(((t - period / 4) * (2 * Math.PI)) / period) +
      1
    );
  }

  function onTypewriterComplete() {
    typewriterComplete = true;
    setTimeout(() => {
      showName = true;
      showFinalImage = true;

      setTimeout(() => {
        showNextButton = true;
      }, 1500);
    }, 200);
  }

  function startAnimation() {
    if (!hasStarted) {
      hasStarted = true;

      setTimeout(() => {
        peekState = "hidden";
        setTimeout(() => {
          startPeekSequence();
        }, 100);
      }, 0);
    }
  }

  function startPeekSequence() {
    peekState = "peekBottom";

    setTimeout(() => {
      peekState = "hidden";
      showGreeting = true;
    }, 2000);
  }
</script>

<svelte:head>
  <style>
    body {
      overflow: hidden;
    }
  </style>
</svelte:head>

<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
<main class:image-active={showFinalImage}>
  {#if !hasStarted}
    <Button onClick={startAnimation}>Start</Button>
  {:else}
    <div class="content-wrapper" class:slide-up={showFinalImage}>
      {#if showGreeting}
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
      {/if}
    </div>

    {#if peekState === "peekBottom"}
      <div
        class="image-wrapper peek-bottom"
        in:fly|local={{ y: 200, duration: 1000, easing: (t) => t * t * t }}
        out:fly|local={{ y: 200, duration: 250 }}
      >
        <enhanced:img src={profilePicture} height="250"></enhanced:img>
      </div>
    {/if}

    {#if showFinalImage}
      <div
        class="final-image"
        in:fly={{ y: 150, duration: 750, easing: gentleElasticOut }}
      >
        <enhanced:img src={profilePicture} height="250"></enhanced:img>
      </div>
    {/if}

    {#if showNextButton}
      <div class="next-button-container" in:fade={{ duration: 250 }}>
        <Button href="/slide/1">Next</Button>
      </div>
    {/if}
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
    20% {
      transform: translateY(-24px);
      opacity: 1;
    }
    40% {
      transform: translateY(0px);
    }
    60% {
      transform: translateY(-6px);
    }
    80% {
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

  .next-button-container {
    position: absolute;
    bottom: 40px;
    right: 40px;
    z-index: 10;
  }
</style>
