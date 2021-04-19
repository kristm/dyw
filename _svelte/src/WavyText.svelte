<script>
  export let name;  
</script>
<svg width="100%" height="60px" viewBox="0 0 500 100" class="speaker-name" style="overflow: overlay">
  <path id="curve" fill="transparent" d="M1.576,93.406c109.438,53.148 406.493,-134.671 487.766,-82.656"></path>
  <text width="100%" style="transform:translate3d(0,0,0);">
      <textPath style="transform:translate3d(0,0,0);" alignment-baseline="top" xlink:href="#curve" startOffset="60px" class="curve-path">{name}</textPath>
  </text>
</svg>
<style lang="stylus">
  text
    font-size 3rem
    font-family "Yellowtail"
    fill #272C65
</style>
