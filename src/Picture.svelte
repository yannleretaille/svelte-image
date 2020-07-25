<script>
  export let alt = ''
  export let height
  export let load
  export let loaded
  export let placeholder = true
  export let sizes
  export let srcset = ''
  export let srcsetWebp = ''
  export let width

  let className
  export { className as class }
</script>

<style>
  .placeholder {
    opacity: 0;
    transition: opacity 0.5s ease;
    transition-delay: 0.7s;
  }

  .loaded {
    opacity: 1;
  }
</style>

<!-- todo: could factor in different crops -->
<picture>
  {#if srcsetWebp}
    <source {sizes} srcset={srcsetWebp} type="image/webp" />
  {/if}
  <source {sizes} {srcset} />
  <img
    {alt}
    class={className}
    class:loaded
    class:placeholder
    {height}
    src=""
    use:load
    {width} />
</picture>
