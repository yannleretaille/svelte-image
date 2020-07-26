<script>
  export let lazy
  export let isServer
</script>

{#if isServer && lazy}
  <noscript>
    <slot />
  </noscript>
{:else}
  <slot />
{/if}
