<script>
  export let letter;
  export let X;
  export let Y;
  export let onClickLetter;
  export let isCorrectRuneNumber;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div 
  class={`floating-script ${isCorrectRuneNumber ? "gold-on-hover" : "shake-on-hover" } glow`}
  style="--X:{X}; --Y:{Y}"
  on:click={onClickLetter}>
  {letter}
</div>

<style>
  .floating-script{
    position: absolute;
    width: min-content;
    max-height: 50px;
    overflow: hidden;

    left: var(--X);
    top: var(--Y);

    font-family: 'noto-sans-medefaidrin, Courier New, Courier, monospace';
    font-size: 50px;
    line-height: 50px;
    color: #BBB;
    -webkit-text-stroke-width: "1px";
    -webkit-text-stroke-color: #126600;
    text-align: center;
    
    cursor: pointer;

    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
    -khtml-user-select: none; /* Konqueror HTML */
    -moz-user-select: none; /* Old versions of Firefox */
    -ms-user-select: none; /* Internet Explorer/Edge */
    user-select: none; /* Non-prefixed version, currently supported by Chrome, Edge, Opera and Firefox */
  }

  .shake-on-hover:hover {
    color: black;
    opacity:50%;

    animation: shake 0.1s;
    -webkit-animation: shake 0.1s;
    -moz-animation: shake 0.1s;
  }

  .gold-on-hover:hover{
    animation: gold-glow 4s linear 0s infinite reverse;
    -webkit-animation: gold-glow 4s linear 0s infinite reverse;
    -moz-animation: gold-glow 4s linear 0s infinite reverse;
  }

  .glow {
    animation: glow 4s linear 0s infinite reverse;
    -webkit-animation: glow 4s linear 0s infinite reverse;
    -moz-animation: glow 4s linear 0s infinite reverse;
  }

  @font-face {
    font-family: noto-sans-medefaidrin;
    src: url("../assets/NotoSansMedefaidrin.ttf");
  }

  @keyframes glow {
    0% {
      text-shadow: 0 0 10px #00CCFF; opacity: 40%;
    }
    30%{
      text-shadow: 0 0 2px #0088DD; opacity: 90%;
    }
    70%{
      text-shadow: 0 0 2px #0088DD; opacity: 90%;
    }
    100% {
      text-shadow: 0 0 10px #00CCFF; opacity: 40%;
    }
  }

  @keyframes gold-glow {
    0% {
      text-shadow: 0 0 10px #FADE33; opacity: 40%;
    }
    30%{
      text-shadow: 0 0 2px #DAAD00; opacity: 90%;
    }
    70%{
      text-shadow: 0 0 2px #DAAD00; opacity: 90%;
    }
    100% {
      text-shadow: 0 0 10px #FADE33; opacity: 40%;
    }
  }
  
  @keyframes shake{
    0%{
      transform: translateX(0);
    }
    25%{
      transform: translateX(10px);
    }
    50%{
      transform: translateX(-10px);
    }
    100%{
      transform: translateX(0px);
    }
  }
</style>
  