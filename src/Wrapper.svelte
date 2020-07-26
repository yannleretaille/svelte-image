<script>
  export let alt
  export let loaded
  export let placeholder
  export let placeholderClass
  export let ratio
  export let src
  export let wrapperClass
</script>

<style>
  .wrapper {
    position: relative;
  }

  .placeholder,
  .ratio :global(img) {
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    will-change: opacity;
  }

  .placeholder {
    opacity: 1;
    transition: opacity 0.5s ease;
    transition-delay: 0.7s;
  }

  .loaded .placeholder {
    opacity: 0;
  }
</style>

{#if placeholder || ratio}
  <div
    class="wrapper {wrapperClass}"
    class:loaded
    class:ratio
    style={ratio && `padding-bottom:${ratio};`}>
    {#if placeholder}
      <img {alt} class="placeholder {placeholderClass}" {src} />
    {/if}

    <slot />
  </div>
{:else}
  <slot />
{/if}
