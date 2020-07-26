<script>
  import { createEventDispatcher } from 'svelte'
  import Waypoint from 'svelte-waypoint'

  export let lazy
  export let offset
  export let waypointClass

  const dispatch = createEventDispatcher()

  function onenter() {
    dispatch('enter')
  }
</script>

{#if lazy}
  <Waypoint class={waypointClass} {offset} once on:enter={onenter}>
    <slot />
  </Waypoint>
{:else}
  <slot />
{/if}
