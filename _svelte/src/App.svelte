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
      pin: true,
      toggleActions: "restart none reverse pause",
    });

    console.log(">> ", document.querySelector("#bg-wrap"));
    scene1.to("#bg-wrap", { yPercent: 40, duration: 1 }, 0).to("#bg-wrap", {opacity:0, duration: 0},1);
  });
</script>
<template lang="pug">
  main
    h1 hello #{name} :metal:

    div(class='bg' id='bg-wrap')
      - for (var i=0; i<4; i++)
        div(class='bg'+i)

    footer
</template>
<style lang="stylus">
	main
    height 3000px
    position relative
    border: 5px solid blue

  footer
    height 600px
    width 100%
    border 5px solid green
    position absolute
    bottom 0

  .bg {
    border: 5px solid red;
    width: 100%;
    height: 50%;
    position: absolute;
    top: -500px;

    > div {
      width: 100%;
      height: 100%;
      position: absolute;
      bottom: 0;
      background-position: bottom center;
      background-repeat: no-repeat;
    }
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
