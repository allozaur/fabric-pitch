<script lang="ts">
  interface SvgItemProps {
    name?: string;
  }

  const assetsPath = "../../assets/svg/";

  const assets = import.meta.glob("../../assets/svg/*.svg", {
    query: "?raw",
    import: "default",
    eager: true,
  });

  let { name }: SvgItemProps = $props();
</script>

<div class="svg-item">
  {@html assets[`${assetsPath}${name}.svg`]}
</div>

<style lang="postcss">
  .svg-item {
    display: contents;
    font-size: var(--size, 2rem);
  }

  .svg-item :global(svg) {
    height: 1em;
    width: auto;
  }
</style>
