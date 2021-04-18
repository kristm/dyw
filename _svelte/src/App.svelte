<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
	export let name;

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    let scene1 = gsap.timeline(); // TODO: add callback to return to original Y position (-500)
    ScrollTrigger.create({
      animation: scene1,
      trigger: "#bg-wrap",
      start: "top top",
      end: "45%",
      scrub: 1,
    });

    scene1.to("#bg-wrap", { yPercent: 150, duration: 2 }, 0);
    scene1.to("#bg-wrap", {opacity:0, duration: 1},1);

    let footerAnimProps = {
      trigger: "footer",
      toggleActions: "restart none reverse none",
      start: "top bottom",
      end: "+=400px",
      scrub: .5,
    };
    gsap.from("footer .bg0", { scrollTrigger: footerAnimProps, y: 100, duration: 1 })
    gsap.to("footer .bg1", { scrollTrigger: footerAnimProps, y: 10, duration: .5 })
    gsap.to("footer .bgtree", { scrollTrigger: footerAnimProps, y: -200, duration: 1, delay: 1 })
  });
</script>
<template lang="pug">
  .wrapper
    header
      h1

      div(id='bg-wrap')
        .bg.bgtree
        - for (var i=0; i<4; i++)
          div(class='bg bg'+i)

    main
    footer
      .bg.bgtree
      - for (var i=0; i<2; i++)
        div(class='bg bg'+i)
</template>
<style lang="stylus">
  .wrapper
    position relative
    overflow hidden
    background-color #A7DED9

  header
    position absolute
    top 0
    width 100%
    height 1000px
    z-index 2

  main
    //border 5px solid yellow
    position relative
    top 500px
    width 100%
    height 4000px
    background url('/images/clouds.png') no-repeat top center
    background-size 100%
    z-index 1

  #bg-wrap {
    //border 5px solid green
    height 1000px 
    position relative
    top 0

    & > .bgtree {
      top 10px 
    }
  }

  .bg {
    //border 2px solid blue
    width: 100%;
    height: 100%;
    position: absolute;
    background-position: bottom center;
    background-repeat: no-repeat;
  }


  for num in (0..3)
    .bg{num}
      background-image url('/images/bg'+num+'.png')

  .bgtree
    background-image url('/images/bgtree.png')
    top 300px


  footer
    //border 2px solid black
    width 100%
    height 400px
    position absolute
    bottom 0

    & > .bg
      background-position top center

    #bg-footer
      position absolute
      top 60%
      width 100%
      height 100%

      & > .bg
        background-position top center

	@media (min-width: 640px)
		main
			max-width none
</style>
