<script>
  import { gsap } from 'gsap';
	export let name;

  gsap.registerPlugin(ScrollTrigger);
</script>

<template lang="pug">
  main
    h1 hello #{name} :metal:

    - for (var i=0; i<4; i++)
      div(class='bg bg'+i)

</template>
<style lang="stylus">
	main
    height 2000px

  .bg {
    width: 100%;
    background-position: bottom center;
    background-repeat: no-repeat;
  }

  .bg0 {
    background-image: url(/images/bg0.png);
    height: 100%;
  }

  .bg1 {
    background-image: url(/images/bg1.png);
    height: 100%;
  }

	@media (min-width: 640px)
		main
			max-width none
</style>
