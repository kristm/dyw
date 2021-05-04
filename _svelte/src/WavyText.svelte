<script>
  export let name;  
</script>
<svelte:head>
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Yellowtail&display=swap" rel="stylesheet">
</svelte:head>
<svg width="100%" height="60px" viewBox="0 0 500 100" class="speaker-name" style="overflow: overlay">
  <path id="curve" fill="transparent" d="M1.576,93.406c109.438,53.148 406.493,-134.671 487.766,-82.656"></path>
  <text width="100%" style="transform:translate3d(0,0,0);">
      <textPath style="transform:translate3d(0,0,0);" alignment-baseline="top" xlink:href="#curve" startOffset="50px" class="curve-path">{name}</textPath>
  </text>
</svg>
<style lang="stylus">
  @font-face
      font-family 'Milkshake'
      font-style normal
      font-weight 400
      font-display swap
      src url("/fonts/Milkshake.woff")
      src url("/fonts/Milkshake.woff2")

  svg
    overflow visible!important

  text
    font-size 3rem
    font-family Yellowtail, Milkshake
    fill #272C65

    @media (min-width: 1400px)
      font-size 3.5rem
</style>
