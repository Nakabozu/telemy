<script>
    export let onClickCobblestone;
</script>

<svg class="cobblestone-clickable" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="27" height="21" viewBox="0 0 27 21" xml:space="preserve">
    <!-- svelte-ignore a11y-missing-attribute -->
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <a on:click={()=>{onClickCobblestone()}}>
        <g transform="matrix(1 0 0 1 13.65 10.81)" id="kcENvRLr9ATmkdbSTHhbr">
            <path style="stroke: rgb(0,0,0); stroke-width: 0; stroke-dasharray: none; stroke-linecap: butt; stroke-dashoffset: 0; stroke-linejoin: miter; stroke-miterlimit: 4; fill: rgb(0,0,0); fill-rule: nonzero; opacity: 1;" vector-effect="non-scaling-stroke"  transform=" translate(0, 0)" d="M -9.38567 10.52332 L -13.367469999999999 5.40387 L -1.4220799999999993 -10.523319999999998 L 13.36745 -10.523319999999998 L 9.95448 10.523320000000002 z" stroke-linecap="round" />
        </g>
    </a>
</svg>

<style>
    .cobblestone-clickable{
      position: absolute;
      width: 55px;
      height: 42px;
  
      top: 248px;
      left: 597px;

      opacity: 0%;
    }
  </style>
  