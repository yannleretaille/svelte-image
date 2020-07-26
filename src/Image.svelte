<script>
  import { createEventDispatcher } from 'svelte'
  import Noscript from './Noscript.svelte'
  import Picture from './Picture.svelte'
  import Waypoint from './Waypoint.svelte'
  import Wrapper from './Wrapper.svelte'

  export let alt = ''
  export let height = null
  export let lazy = true
  export let offset
  export let placeholder = true
  export let placeholderClass = ''
  export let sizes
  export let src = ''
  export let srcset
  export let srcsetWebp
  export let width = null
  export let waypointClass = ''
  export let wrapperClass = ''

  let className = ''
  export { className as class }

  export let ratio = !width && '100%'

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

<Waypoint {offset} {lazy} on:enter={onenter} {waypointClass}>
  <Wrapper
    {alt}
    {loaded}
    {placeholder}
    {placeholderClass}
    {ratio}
    {src}
    {wrapperClass}>
    <Noscript {lazy} {isServer}>
      <Picture
        {alt}
        class={className}
        {entered}
        {height}
        {loaded}
        on:load={onload}
        {placeholder}
        {sizes}
        {srcset}
        {srcsetWebp}
        {width} />
    </Noscript>
  </Wrapper>
</Waypoint>
