<script>
  export let alt = ''
  export let blur = false
  export let height = null
  export let image
  export let load
  export let loaded = false
  export let placeholder = true
  export let sizes = ''
  export let srcset = ''
  export let srcsetWebp = ''
  export let width = null

  let className = ''
  export { className as class }
</script>

<style>
  .blur {
    filter: blur(10px);
    transition: opacity 0.4s ease, filter 0.5s ease;
  }

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
    bind:this={image}
    class="image {className}"
    class:blur
    class:loaded
    class:placeholder
    {height}
    src=""
    use:load
    {width} />
</picture>
