<script>
  import { onMount, tick } from 'svelte';
  import { gsap } from 'gsap';
  import Loader from './Loader.svelte';
  import WavyText from './WavyText.svelte';
  export let title;
  let y;
  let loaded = false;
  const speakers = [
    {name: 'Noel Macatangay', thumb: 'noel'},
    {name: 'Jane Barba', thumb: 'jane'},
    {name: 'Yoj Vestudio', thumb: 'yoj'},
    {name: 'Gerard Cruz', thumb: 'gerard'},
    {name: 'Agung Yuliaji', thumb: 'agung'},
    {name: 'Gifa Eriyanto', thumb: 'gifa'},
    {name: 'Ann Pauline Lim', thumb: 'ann'},
    {name: 'Francis Tolentino Jr.', thumb: 'francis'},
    {name: 'Justus Tumacder', thumb: 'justus'},
    {name: 'Carlo Joseph Moskito', thumb: 'carlo'},
    {name: 'Gregorious Gesta', thumb: 'gesta'},
    {name: 'Zyra Reambonanza', thumb: 'zyra'}
  ];
  const isChrome = !!window.chrome;

  gsap.registerPlugin(ScrollTrigger);

  const gsapInit = async () => {
    await tick(); //ensure that DOM is ready for gsap
    gsap.set("h1", {opacity: 1});
    gsap.utils.toArray("li").forEach((speaker, i) => {
      gsap.set(speaker, {
        y: gsap.utils.random(-100, 100),
      });
    });

    let scene1 = gsap.timeline(); // TODO: add callback to return to original Y position (-500)
    ScrollTrigger.create({
      animation: scene1,
      trigger: "#bg-wrap",
      start: "top",
      end: "45%",
      markers: false,
      scrub: 3,
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
    scene1.to(".fg__pink", { xPercent: -100, yPercent: 90, duration: 1 }, 0.1);
    scene1.to(".fg__yellow", fgLeftProps, 0.1);
    scene1.to(".fg__ryellow", fgRightProps,0.1);
    scene1.to(".fg__rbyellow", fgRightProps, 0.15);
    scene1.to(".title-pre", { opacity: 0, duration: 0.2 }, 0);
    scene1.to("#bg-wrap", { yPercent: 200, duration: 2 }, 0);
    scene1.to("#bg-wrap", {opacity:0, duration: 0.5},1);

    let titleAnimProps = {
      trigger: "h1",
      toggleActions: "restart none reverse none",
      start: "top 20%",
      end: "+=2000",
      pin: true,
      scrub: 1,
    };
    gsap.to("h1", { scrollTrigger: titleAnimProps, scale: 1.4, duration: 2 })
      
    let h2AnimProps = {
      trigger: "h2",
      start: "top bottom",
      end: "top",
      ease: "power2",
      scrub: 1,
      markers: false,
    };

    function unwrap() {
      let h2 = document.querySelector("h2")
      if (h2 && isChrome) {
        h2.classList.add("glow")
      }

      let angle = Math.round(y/100+y/10-100)

      const lightColors = ["rgb(212, 186, 211)", "rgb(24, 219, 241)"] // pink/light blue
      //const lightColors = ["rgb(189, 18, 142)", "rgb(24, 219, 241)"] // pink/deep blue
      const darkColors = ["rgb(16, 18, 42)", "rgb(24, 219, 241)"]
      const colors = isChrome ? darkColors : lightColors;
        
      gsap.to("h2", { scrollTrigger: h2AnimProps, backgroundImage: "linear-gradient("+angle+"deg, "+colors[0]+", "+colors[1], duration: 3 })
      const spans = document.querySelectorAll("h2 span")
        spans.forEach((el) => {
          el.outerHTML = el.innerHTML
        })
    }

    ScrollTrigger.batch("h2 span", {
      interval: 1,
      batchMax: 2,
      start: "top bottom",
      end: "top 10%",
      ease: "power3",
      markers: false,
      onEnter: batch => gsap.to(batch, {y: 0, opacity: 1, color: "#272C65", duration: 1.5, stagger: 0.2}),
    });

    function vrotate() {
      const dir = ["+", "-"];
      return dir[Math.round(gsap.utils.random(0,1))]+"="+gsap.utils.random(0,2);
    }

    function vdir(max=2) {
      const dir = ["+", "-"];
      return dir[Math.round(gsap.utils.random(0,1))]+"="+Math.round(gsap.utils.random(0,max));
    }


    ScrollTrigger.batch("li", {
      interval: 1,
      batchMax: 2,
      onEnter: batch => gsap.to(batch, {y: () => vdir(20), rotation: vrotate, duration: 1.5, stagger: 0.5}),
      onEnterBack: batch => gsap.to(batch, {y: () => vdir(10), rotation: 0, duration: 1.5, stagger: 0.5}),
    });

    ScrollTrigger.batch(".speaker-name", {
      interval: 1,
      batchMax: 2,
      onEnter: batch => { gsap.to(batch, {y: vdir, duration: 1, stagger: 0.5}); unwrap() },
      onEnterBack: batch => gsap.to(batch, {y: vdir, duration: 1, stagger: 0.5}),
    });

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
  };
</script>
<svelte:window on:load={() => { loaded = true; gsapInit() }} bind:scrollY={y}/>
<svelte:head>
  <title>{title}</title>
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Yellowtail&display=swap" rel="stylesheet">
</svelte:head>
<template lang="pug">
  .wrapper
    +if('loaded')
      header
        h1 {title}
        div(id='bg-wrap')
          .bg.bgtree
          - for (var i=0; i<4; i++)
            div(class='bg bg'+i)

        div(id='fg-wrap')
          each val in ['pink', 'green', 'yellow', 'ryellow', 'rbyellow']
            div(class='fg fg__'+val)

        .title-pre

      main
        h2 
          span Distribute Your Wisdom is a virtual conference 
          span from members of the Quipper Global<br> 
          span Team. The current pandemic situation has 
          span challenged all of us in our work and everyday lives.
          span But it also became an opportunity for growth and 
          span discovery. <br>Join us in a week of knowledge sharing!

        h3 Speakers
        ul
          +each('speakers as {name, thumb}')
            li
              img(src="/dyw/assets/images/speaker_{thumb}.jpg")
              WavyText(name="{name}")

      footer
        .bg.bgtree
        - for (var i=0; i<2; i++)
          div(class='bg bg'+i)

      <svg width="0" height="0">
        <defs>
          <clipPath id="clipMask">
            <path fill="#ffffff" stroke="#000000" stroke-width="1" stroke-miterlimit="5" d="M86.257,23.112c-0,-12.756 10.356,-23.112 23.112,-23.112c12.756,0 23.113,10.356 23.113,23.112c6.378,-11.047 20.525,-14.837 31.572,-8.459c11.047,6.378 14.837,20.525 8.459,31.572c11.048,-6.378 25.195,-2.588 31.573,8.46c6.378,11.047 2.587,25.194 -8.46,31.572c12.756,-0 23.112,10.356 23.112,23.112c0,12.756 -10.356,23.113 -23.112,23.113c11.047,6.378 14.838,20.525 8.46,31.572c-6.378,11.047 -20.525,14.837 -31.573,8.459c6.378,11.048 2.588,25.195 -8.459,31.573c-11.047,6.378 -25.194,2.587 -31.572,-8.46c-0,12.756 -10.357,23.112 -23.113,23.112c-12.756,0 -23.112,-10.356 -23.112,-23.112c-6.378,11.047 -20.525,14.838 -31.572,8.46c-11.048,-6.378 -14.838,-20.525 -8.46,-31.573c-11.047,6.378 -25.194,2.588 -31.572,-8.459c-6.378,-11.047 -2.588,-25.194 8.459,-31.572c-12.756,-0 -23.112,-10.357 -23.112,-23.113c0,-12.756 10.356,-23.112 23.112,-23.112c-11.047,-6.378 -14.837,-20.525 -8.459,-31.572c6.378,-11.048 20.525,-14.838 31.572,-8.46c-6.378,-11.047 -2.588,-25.194 8.46,-31.572c11.047,-6.378 25.194,-2.588 31.572,8.459Z"/>
          </clipPath>
        </defs>
      </svg>
      +else
        Loader

</template>
<style lang="stylus">
  skyblue = #A7DED9

  :global(body)
    background-color skyblue

  @font-face
    font-family 'NoWorries'
    font-style normal
    font-weight 400
    font-display swap
    src url("/dyw/assets/fonts/NoWorries.woff")
    src url("/dyw/assets/fonts/NoWorries.woff2")

  .wrapper
    border none
    margin auto
    position relative
    overflow hidden
    background-color skyblue

  header
    //border 5px solid red
    width 100%
    height 1000px
    z-index 2

    h1, .title-pre
      width 100%
      height 30vh
      position absolute
      top 40vh
      color transparent
  h1
    background url('/dyw/assets/images/title.svg') no-repeat top center
    opacity 0

  h2
    font-size 3rem
    width 90%
    color white
    margin 100vh auto
    font-family Yellowtail
    color #272C65

    span
      color skyblue
      opacity 0
      display block
      transform translate(0, 100%)

  .title-pre
    filter blur(2px)
    transform scale(.5)
    background url('/dyw/assets/images/title_pre.svg') no-repeat top center

  main
    //border 5px solid yellow
    width 100%
    padding 2000px 0 500px
    background url('/dyw/assets/images/clouds.png') no-repeat top center
    background-size 100%
    text-align center
    z-index 1

    h3
      font-family NoWorries
      font-size 4rem
      margin 500px 0

    ul
      //border 2px solid white
      display flex
      width 80%
      margin 0 auto
      flex-wrap wrap
      list-style-type none
      justify-content space-between
      background url('/dyw/assets/images/clouds.png') no-repeat top center
      background-size contain

    li
      font-size 2rem
      text-align center
      margin 15rem 2rem
      display flex
      flex-direction column

    img
      width: 218px
      height: 218px
      clip-path: url(#clipMask)

  #fg-wrap
    width 100%
    height 80vh
    position absolute
    top 40vh

  .fg {
    background-repeat no-repeat
    background-size 90%
    width 50vh
    height 100%
    position absolute

    &__pink {
      background-image url('/dyw/assets/images/left_pink.png')
      background-position bottom left
      bottom 0
    }

    &__yellow {
      background-image url('/dyw/assets/images/left_yellow.png')
      background-position top left
      top 40% 
    }

    &__ryellow {
      background-image url('/dyw/assets/images/right_yellow.png')
      background-position top right
      background-size 80%
      height 70%
      bottom 0
      right -20px
    }

    &__rbyellow {
      background-image url('/dyw/assets/images/right_bottom_yellow.png')
      background-position top right
      height 70%
      bottom -50px
      right -20px
    }

    &__green {
      background-image url('/dyw/assets/images/left_green.png')
      background-position -50px 0
      top 20%
    }
  }


  #bg-wrap {
    //border 5px solid green
    height 1000px 
    position relative
    transform-box view-box
    //bottom -200px

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
      background-image url('/dyw/assets/images/bg'+num+'.png')

  .bgtree
    background-image url('/dyw/assets/images/bgtree.png')
    top 300px


  footer
    //border 2px solid black
    width 100%
    height 400px
    position absolute
    bottom 0

    & > .bg
      background-position top center

  @media (min-width: 640px)
    main
      ul
        justify-content space-around
      li
        margin 10rem 0

      h3
        font-size 3rem

    #fg-wrap .fg__pink
      display none

  @media (min-width: 800px)
    #fg-wrap .fg__pink
      display unset

    main
      ul
        width 100%
      li
        margin 10rem 5rem


  @media (min-width: 1400px)
    h2
      width: 60%

    main
      h3
        font-size 4.5rem


  @media (min-width: 1900px)
    h2
      width: 50%

    .wrapper
      max-width 1500px
      border 10px solid white

    #fg-wrap .fg__pink
      display none

    #bg-wrap
      height 100vh
      bottom 0

</style>
