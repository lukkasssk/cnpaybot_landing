<script>
  export let src = '';
  export let trigger = 'hover'; // hover, click, loop, loop-on-hover, morph, morph-two-way
  export let colors = 'primary:#121331,secondary:#08a88a'; // formato: primary:#color,secondary:#color
  export let size = '200px';
  export let style = '';
  export let state = 'hover'; // hover, intro, loop, loop-on-hover, morph, morph-two-way
  export let delay = 0;
  export let speed = 1;
  export let stroke = 'light'; // light, regular, bold
  export let target = '';
  
  let lordIconElement;
  
  import { onMount } from 'svelte';
  
  onMount(() => {
    if (lordIconElement && window.lottie) {
      // O Lord Icon será carregado automaticamente pelo CDN
    }
  });
</script>

<lord-icon
  bind:this={lordIconElement}
  src={src}
  trigger={trigger}
  colors={colors}
  style="width:{size}; height:{size}; {style}"
  state={state}
  delay={delay}
  speed={speed}
  stroke={stroke}
  target={target}
>
</lord-icon>

<style>
  lord-icon {
    display: inline-block;
  }
</style> 