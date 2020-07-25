<script>
  // import Waypoint from 'svelte-waypoint'
  import LazyNoscript from './LazyNoscript.svelte'
  import Picture from './Picture.svelte'
  import Wrapper from './Wrapper.svelte'

  export let lazy = true

  // export let ratio = '100%'
  // export let blur = false
  // export let sizes = '(max-width: 1000px) 100vw, 1000px'
  // export let threshold = 1.0
  // export let wrapperClass = ''
  // export let placeholderClass = ''
  // export let placeholder = true

  // let className = ''
  // export { className as class }

  // const sizeString = sizes.map()

  let loaded = !lazy
  function load(img) {
    img.onload = () => (loaded = true)
  }
</script>

<Wrapper {...$$restProps} {loaded}>
  <LazyNoscript {lazy}>
    <Picture {...$$restProps} {load} {loaded} />
  </LazyNoscript>
</Wrapper>

<!-- <Waypoint
  class={wrapperClass}
  style="min-height: 100px; width: 100%;"
  once
  {threshold}
  disabled={!lazy}>
</Waypoint> -->
