<script lang="ts">
  import type { Snippet } from "svelte";

  interface ButtonProps {
    label?: string;
    href?: string;
    children?: Snippet;
    onClick?: (event: MouseEvent) => void;
  }

  let { children, href, label, onClick }: ButtonProps = $props();
</script>

{#snippet buttonInner()}
  {#if typeof children === "function"}
    {@render children()}
  {:else if label}
    {label}
  {/if}
{/snippet}

{#if href}
  <a class="button" {href} onclick={onClick}>
    {@render buttonInner()}
  </a>
{:else}
  <button class="button" onclick={onClick}>
    {@render buttonInner()}
  </button>
{/if}

<style>
  .button {
    border: none;
    cursor: pointer;
    font-size: 1.25rem;
    color: var(--c-text);
    font-weight: 600;
    letter-spacing: 0.01rem;
    padding: 1.25rem 2rem;
    background: var(--bg-surface-0);
    border-radius: 0.5rem;
    text-decoration: none;
  }
</style>
