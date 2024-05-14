<script>
  import { onMount } from 'svelte';
  import '../global.css'
  import Particles, { particlesInit } from '@tsparticles/svelte';
   import { loadSlim } from '@tsparticles/slim';
  let rotation = 0;

  onMount(() => {
    document.title = 'Cosmo - Próximamente';
    const interval = setInterval(() => {
      rotation = (rotation + 1) % 360;
    }, 100);

    return () => {
      clearInterval(interval);
    };
  });

   // @ts-ignore
   let particlesUrl = 'http://foo.bar/particles.json'; // placeholder, replace it with a real url

    // @ts-ignore
    let particlesConfig = {
        particles: {
            color: {
                value: '#000'
            },
            links: {
                enable: true,
                color: '#000'
            },
            move: {
                enable: true
            },
            number: {
                value: 100
            }
        }
    };

    // @ts-ignore
    let onParticlesLoaded = (event) => {
        // @ts-ignore
        const particlesContainer = event.detail.particles;

        // you can use particlesContainer to call all the Container class
        // (from the core library) methods like play, pause, refresh, start, stop
    };

    void particlesInit(async (engine) => {
        // call this once per app
        // you can use main to customize the tsParticles instance adding presets or custom shapes
        // this loads the tsparticles package bundle, it's the easiest method for getting everything ready
        // starting from v2 you can add only the features you need reducing the bundle size
        //await loadFull(engine);
        await loadSlim(engine);
    });
</script>

<style>
  .coming-soon {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-size: 2em;
    font-weight: bold;
    color: white;
    transition: transform 1s;
    text-align: center;
  }
</style>

<div class="coming-soon" style="transform: rotate({rotation}deg);">
  Próximamente
  <br/>
  El universo a tu servicio
</div>
<Particles id="tsparticles" options="{particlesConfig}" on:particlesLoaded="{onParticlesLoaded}" />

