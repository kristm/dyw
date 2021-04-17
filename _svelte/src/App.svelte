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
      markers: true,
      onEnterBack: function() { gsap.to("#bg-wrap", { yPercent: 0, opacity: 1, duration: 2 }, 0); console.log("hey asshole");  },
      onEnter: function () { console.log("OK") },
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
    gsap.from("footer .bg1", { scrollTrigger: footerAnimProps, y: 50, duration: .5 })
  });
</script>
<template lang="pug">
  main
    header
    h1 hello #{name} :metal:

    div(id='bg-wrap')
      - for (var i=0; i<4; i++)
        div(class='bg bg'+i)

    footer
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
    border 5px solid yellow

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

	@media (min-width: 640px)
		main
			max-width none
</style>
