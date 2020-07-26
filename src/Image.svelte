<script>
  import { createEventDispatcher } from 'svelte'
  import Noscript from './Noscript.svelte'
  import Picture from './Picture.svelte'
  import Waypoint from './Waypoint.svelte'
  import Wrapper from './Wrapper.svelte'
  import Bear from '../../roo/src/components/animals/Bear.svelte'

  export let alt = ''
  export let lazy = true
  export let placeholder = true

  const dispatch = createEventDispatcher()

  // always load srcset's in ssr -> always noscript wrapped or non lazy
  const isServer = typeof process !== 'undefined'
  let entered = isServer ? true : !lazy
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

<Waypoint {...$$restProps} {lazy} on:enter={onenter}>
  <Wrapper {...$$restProps} {alt} {isServer} {loaded} {placeholder}>
    <Noscript {isServer} {lazy}>
      <Picture
        {...$$restProps}
        {alt}
        {entered}
        {loaded}
        on:load={onload}
        {placeholder} />
    </Noscript>
  </Wrapper>
</Waypoint>
