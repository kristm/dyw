<script>
  document.querySelector("#logo_bg");
</script>
<div class="loader">
  <svg id="logo_bg" viewBox="0 0 250 250" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;"><rect id="Artboard2" x="0" y="0" width="250" height="250" style="fill:none;"/><path d="M98.674,26.75c-0,-14.53 11.796,-26.326 26.326,-26.326c14.53,0 26.326,11.796 26.326,26.326c7.265,-12.583 23.379,-16.901 35.962,-9.636c12.583,7.265 16.901,23.379 9.636,35.962c12.583,-7.265 28.697,-2.947 35.962,9.636c7.265,12.583 2.947,28.697 -9.636,35.962c14.53,-0 26.326,11.796 26.326,26.326c-0,14.53 -11.796,26.326 -26.326,26.326c12.583,7.265 16.901,23.379 9.636,35.962c-7.265,12.583 -23.379,16.901 -35.962,9.636c7.265,12.583 2.947,28.697 -9.636,35.962c-12.583,7.265 -28.697,2.947 -35.962,-9.636c0,14.53 -11.796,26.326 -26.326,26.326c-14.53,-0 -26.326,-11.796 -26.326,-26.326c-7.265,12.583 -23.379,16.901 -35.962,9.636c-12.583,-7.265 -16.901,-23.379 -9.636,-35.962c-12.583,7.265 -28.697,2.947 -35.962,-9.636c-7.265,-12.583 -2.947,-28.697 9.636,-35.962c-14.53,0 -26.326,-11.796 -26.326,-26.326c0,-14.53 11.796,-26.326 26.326,-26.326c-12.583,-7.265 -16.901,-23.379 -9.636,-35.962c7.265,-12.583 23.379,-16.901 35.962,-9.636c-7.265,-12.583 -2.947,-28.697 9.636,-35.962c12.583,-7.265 28.697,-2.947 35.962,9.636Z" style="fill:#f5f6f6;"/></svg>
  <svg id="logo_q" viewBox="0 0 236 236" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;"><rect id="Artboard2" x="0" y="0" width="250" height="250" style="fill:none;"/><path d="M171.48,159.26c-0,4.87 -1.25,7.16 -4.25,7.16c-3.89,-0 -6.5,-5.16 -7.38,-10.11c8.55,-9.28 12.89,-22.52 12.89,-38.84c-0,-33.09 -16.47,-55.16 -53.14,-55.16c-31.2,-0 -52.2,22.38 -52.2,54.07c-0,36.67 21.75,55 53.14,55c4.059,0.018 8.112,-0.296 12.12,-0.94c3.19,7.66 11.44,17.25 25.19,17.25c15.54,-0 24.75,-8.82 24.75,-27.44l-0,-5l-11.12,-0l-0,4.01Zm-51.39,-10.87c-13,0 -18.58,-14.35 -18.58,-32c-0,-17.65 5.82,-32 18.58,-32c12.76,-0 18.59,14.25 18.59,31.95c0,17.7 -5.6,32.05 -18.59,32.05Z" style="fill:#00beff;fill-rule:nonzero;"/></svg>
</div>
<style lang="stylus">
  skyblue = #A7DED9

  :global(body)
    background-color skyblue
    display flex
    align-items center
    justify-content center

  .loader
    width 8vh
    height 8vh
    position relative

  svg
    width 100%
    height 100%
  
  #logo_bg
    animation spin 12s linear infinite

  #logo_q
    position absolute
    left -2px 
    top 0

  @keyframes spin
    from
      transform rotate(0)
    to
      transform rotate(360deg)
</style>
