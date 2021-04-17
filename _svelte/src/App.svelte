<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
	export let name;

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    let scene1 = gsap.timeline({yoyo:true}); // TODO: add callback to return to original Y position (-500)
    ScrollTrigger.create({
      animation: scene1,
      trigger: "main",
      start: "top",
      snap: { snapTo: "labels" },
      pin: true,
      toggleActions: "restart none reverse pause",
    });

    console.log(">> ", document.querySelector("#bg-wrap"));
    scene1.addLabel("start").to("#bg-wrap", { yPercent: 40, duration: 1 }, 0).to("#bg-wrap", {opacity:0, duration: 0},1);

    // let scene2 = gsap.timeline();
    // ScrollTrigger.create({
    //   animation: scene2,
    //   trigger: "footer",
    //   start: "top center",
    //   markers: true,
    //   toggleActions: "restart none reverse pause",
    // });

    // scene2.from("footer", { opacity: 0, yPercent: 100 }, 0)
    //       .from("footer dev", { y: 100, stagger: 0.1, duration: 2 }, 0);
    let footerAnimProps = {
      trigger: "#bg-footer",
      toggleActions: "restart none reverse none",
      start: "top",
      end: "bottom",
    };
    gsap.from("footer .bg0", { scrollTrigger: footerAnimProps, y: -800, duration: 1 })
    gsap.from("footer .bg1", { scrollTrigger: footerAnimProps, y: -500, duration: 2 })
  });
</script>
<template lang="pug">
  main
    h1 hello #{name} :metal:

    div(id='bg-wrap')
      - for (var i=0; i<4; i++)
        div(class='bg bg'+i)

    footer
      #bg-footer
        - for (var i=0; i<4; i++)
          div(class='bg bg'+i)
</template>
<style lang="stylus">
	main
    height 3000px
    position relative
    overflow hidden

  footer
    width 100%
    height 30%
    position absolute
    bottom 0 

    #bg-footer
      position absolute
      top 60%
      width 100%
      height 100%

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

  //bspace = ( -6000px -4000px -2000px 0 )

  for num in (0..3)
    .bg{num}
      background-image url('/images/bg'+num+'.png')
      //bottom bspace[num]

	@media (min-width: 640px)
		main
			max-width none
</style>
