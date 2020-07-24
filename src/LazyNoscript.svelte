<script>
  export let lazy
  const isServer = typeof process !== 'undefined'
</script>

{#if isServer && lazy}
  <noscript>
    <slot />
  </noscript>
{:else}
  <slot />
{/if}
