<script>
  import { gsap } from 'gsap';
	export let name;

  gsap.registerPlugin(ScrollTrigger);
</script>

<template lang="pug">
  main
    h1 hello #{name} :metal:

    div(class='bg')
      - for (var i=0; i<4; i++)
        div(class='bg'+i)

</template>
<style lang="stylus">
	main
    height 3000px
    position relative
    border: 5px solid blue

  .bg {
    border: 5px solid red;
    width: 100%;
    height: 50%;
    position: absolute;
    bottom: 0;

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
