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

    let fgLeftProps = {
      xPercent: -100,
      yPercent: 100,
      duration: 1
    };

    let fgRightProps = {
      xPercent: 100,
      yPercent: 100,
      duration: 0.8
    };

    scene1.to(".fg__green", fgLeftProps);
    scene1.to(".fg__yellow", fgLeftProps, 0.1);
    scene1.to(".fg__pink", { yPercent: 100, opacity: 0, duration: 1 }, 0.1);
    scene1.to(".fg__ryellow", fgRightProps,0.1);
    scene1.to(".fg__rbyellow", fgRightProps, 0.15);
    scene1.to(".title-pre", { opacity: 0, duration: 0.2 }, 0);
    scene1.to("#bg-wrap", { yPercent: 150, duration: 2 }, 0);
    scene1.to("#bg-wrap", {opacity:0, duration: 1},1);

    let titleAnimProps = {
      trigger: "h1",
      toggleActions: "restart none reverse none",
      start: "top 20%",
      end: "+=2000",
      pin: true,
      scrub: 1,
    };
    gsap.to("h1", { scrollTrigger: titleAnimProps, scale: 1.2, duration: 2 })

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

      h1 Distrubute your Wisdom. Learn at Work Week. May 24-28 2021
      div(id='bg-wrap')
        .bg.bgtree
        - for (var i=0; i<4; i++)
          div(class='bg bg'+i)

      div(id='fg-wrap')
        each val in ['pink', 'green', 'yellow', 'ryellow', 'rbyellow']
          div(class='fg fg__'+val)

      .title-pre
    main
    footer
      .bg.bgtree
      - for (var i=0; i<2; i++)
        div(class='bg bg'+i)
</template>
<style lang="stylus">
  skyblue = #A7DED9

  :global(body)
    background-color skyblue

  .wrapper
    position relative
    overflow hidden
    background-color skyblue

  header
    position absolute
    top 0
    width 100%
    height 1000px
    z-index 2

    h1, .title-pre
      width 100%
      height 30vh
      position absolute
      top 30vh
      color transparent
  h1
    background url('/images/title.svg') no-repeat top center

  .title-pre
    //opacity 0.5
    filter blur(2px)
    transform scale(.5)
    background url('/images/title_pre.svg') no-repeat top center

  main
    //border 5px solid yellow
    position relative
    top 500px
    width 100%
    height 4000px
    background url('/images/clouds.png') no-repeat top center
    background-size 100%
    z-index 1

  #fg-wrap
    width 100%
    height 80vh
    position absolute
    bottom 0

  .fg {
    background-repeat no-repeat
    background-size 90%
    width 50vh
    height 100%
    position absolute

    &__pink {
      background-image url('/images/left_pink.png')
      background-position bottom left
      bottom 0
    }

    &__yellow {
      background-image url('/images/left_yellow.png')
      background-position top left
      top 40% 
    }

    &__ryellow {
      background-image url('/images/right_yellow.png')
      background-position top right
      background-size 80%
      height 70%
      bottom 0
      right -20px
    }

    &__rbyellow {
      background-image url('/images/right_bottom_yellow.png')
      background-position top right
      height 70%
      bottom -50px
      right -20px
    }

    &__green {
      background-image url('/images/left_green.png')
      background-position top left
      top 20%
    }
  }


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
