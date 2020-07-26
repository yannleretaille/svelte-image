<script>
  import { createEventDispatcher } from 'svelte'
  import Noscript from './Noscript.svelte'
  import Picture from './Picture.svelte'
  import Waypoint from './Waypoint.svelte'
  import Wrapper from './Wrapper.svelte'

  export let lazy = true

  const dispatch = createEventDispatcher()

  let entered = !lazy
  let loaded = entered

  function onload(e) {
    loaded = true
    dispatch('load', e)
  }

  function onenter() {
    entered = true
    dispatch('enter')
  }
</script>

<Waypoint {...$$restProps} on:enter={onenter} {lazy}>
  <Wrapper {...$$restProps} {loaded}>
    <Noscript {lazy}>
      <Picture {...$$restProps} on:load={onload} {entered} {loaded} />
    </Noscript>
  </Wrapper>
</Waypoint>
