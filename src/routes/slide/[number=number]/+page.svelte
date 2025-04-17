<script lang="ts">
  import { page } from "$app/state";
  import { goto } from "$app/navigation";
  import type { Component } from "svelte";
  import WhoAmI from "./WhoAmI.svelte";
  import TechStack from "./TechStack.svelte";
  import ILoveOpenSource from "./ILoveOpenSource.svelte";
  import Brands from "./Brands.svelte";
  import WhatILikeAboutFabric from "./WhatILikeAboutFabric.svelte";
  import Teamwork from "./Teamwork.svelte";
  import Final from "./Final.svelte";

  type PageComponents = {
    [key: string]: {
      component: Component;
    };
  };

  const pages: PageComponents = {
    "1": {
      component: WhoAmI,
    },
    "2": {
      component: Brands,
    },
    "3": {
      component: TechStack,
    },
    "4": {
      component: ILoveOpenSource,
    },
    "5": {
      component: WhatILikeAboutFabric,
    },
    "6": {
      component: Teamwork,
    },
    "7": {
      component: Final,
    },
  };

  const currentPage = $derived(parseInt(page.params.number));

  const nextPage = $derived(currentPage + 1);
  const prevPage = $derived(currentPage - 1);

  function goToPrevPage() {
    if (currentPage === 1) {
      goto("/");
    } else {
      goto(`/slide/${prevPage}`);
    }
  }

  function goToNextPage() {
    if (pages[`${nextPage}`]) {
      goto(`/slide/${nextPage}`);
    }
  }
</script>

<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_static_element_interactions -->
<div class="nav-area left-half" onclick={goToPrevPage}></div>

<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_static_element_interactions -->
<div class="nav-area right-half" onclick={goToNextPage}></div>

{#if pages[`${page.params.number}`]}
  <svelte:component this={pages[`${page.params.number}`].component} />
{:else}
  <h1>Page not found</h1>
{/if}

<span class="page-number">{page.params.number}</span>

<style>
  .nav-area {
    position: fixed;
    top: 0;
    height: 100vh;
    width: 33%;
    z-index: 10;
    cursor: pointer;
  }

  .left-half {
    left: 0;
    cursor: w-resize;
  }

  .right-half {
    right: 0;
    cursor: e-resize;
  }

  .page-number {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    font-size: 1.33rem;
    z-index: 20; /* Ensure it's above the nav areas */
  }
</style>
