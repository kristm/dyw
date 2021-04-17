<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
	export let name;

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    let scene1 = gsap.timeline(); // TODO: add callback to return to original Y position (-500)
    ScrollTrigger.create({
      animation: scene1,
      trigger: "main",
      start: "top top",
      end: "45% 100%",
      onEnterBack: function() { scene1.reverse() },
      onEnter: function () { scene1.play(0) },
    });

    scene1.to("#bg-wrap", { yPercent: 150, duration: 2 }, 0);
    scene1.to("#bg-wrap", {opacity:0, duration: 1},.5);

    let footerAnimProps = {
      trigger: "footer",
      toggleActions: "restart none reverse none",
      start: "top bottom",
      end: "+=400px",
    };
    gsap.from("footer .bg0", { scrollTrigger: footerAnimProps, y: 100, duration: 1 })
    gsap.to("footer .bg1", { scrollTrigger: footerAnimProps, y: 10, duration: .5 })
    gsap.to("footer .bgtree", { scrollTrigger: footerAnimProps, y: -200, duration: 1, delay: 1 })
  });
</script>
<template lang="pug">
  main
    header
    h1 hello #{name} :metal:

    div(id='bg-wrap')
      .bg.bgtree
      - for (var i=0; i<4; i++)
        div(class='bg bg'+i)

    footer
      .bg.bgtree
      - for (var i=0; i<2; i++)
        div(class='bg bg'+i)
</template>
<style lang="stylus">
  *
    padding 0
    margin 0

	main
    height 3000px
    position relative
    overflow hidden

  footer
    width 100%
    height 400px
    position absolute
    bottom 0 

    & > .bg
      background-position top center

    #bg-footer
      border 5px solid red
      position absolute
      top 60%
      width 100%
      height 100%

      & > .bg
        background-position top center

  #bg-wrap {
    width: 100%;
    height: 50%;
    position: absolute;
    top: -500px;

    & > .bgtree {
      top 10px 
    }
  }

  .bg {
    width: 100%;
    height: 100%;
    position: absolute;
    bottom: 0;
    background-position: bottom center;
    background-repeat: no-repeat;
  }


  for num in (0..3)
    .bg{num}
      background-image url('/images/bg'+num+'.png')

  .bgtree
    background-image url('/images/bgtree.png')
    top 300px

	@media (min-width: 640px)
		main
			max-width none
</style>
