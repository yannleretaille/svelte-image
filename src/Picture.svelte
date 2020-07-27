<script>
  import { createEventDispatcher } from 'svelte'

  export let alt = ''
  export let entered
  export let height = null
  export let loaded
  export let placeholder
  export let sizes
  export let srcset
  export let srcsetWebp
  export let width = null

  let className = ''
  export { className as class }

  const dispatch = createEventDispatcher()

  function onload(e) {
    dispatch('load', e)
  }
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

<picture>
  {#if srcsetWebp}
    <source {sizes} srcset={entered ? srcsetWebp : ''} type="image/webp" />
  {/if}
  <source {sizes} srcset={entered ? srcset : ''} />
  <img
    {alt}
    class={className}
    class:loaded
    class:placeholder
    {height}
    on:load={onload}
    src=""
    {width} />
</picture>
