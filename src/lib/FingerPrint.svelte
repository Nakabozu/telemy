<script>
    import {onMount} from "svelte";
    import fingerprint from "../assets/fingerprint.png";

    export let X;
    export let Y;
    let rotation = 0;

    onMount(async () => {
        rotation = Math.floor(Math.random() * 30) + 1;
        if( (Math.floor(Math.random() * 2)) % 2 === 0 ){
            rotation = 360 - rotation;
        }
    })
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="finger-print" style="--X:{(X-50)+"px"}; --Y:{(Y-50)+"px"}; --rotation:{rotation+"deg"};">
   <img src={fingerprint} alt="finger-pring" class="finger-pring-img" draggable="false"/>
</div>

<style>
    .finger-print{
        position: absolute;
        height: min-content;
        width: min-content;
        overflow: hidden;

        left: var(--X);
        top: var(--Y);

        transform: rotate(var(--rotation));

        -webkit-touch-callout: none; /* iOS Safari */
        -webkit-user-select: none; /* Safari */
        -khtml-user-select: none; /* Konqueror HTML */
        -moz-user-select: none; /* Old versions of Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
        user-select: none; /* Non-prefixed version, currently supported by Chrome, Edge, Opera and Firefox */
    }

    .finger-pring-img{
        height: 100px;

        -webkit-touch-callout: none; /* iOS Safari */
        -webkit-user-select: none; /* Safari */
        -khtml-user-select: none; /* Konqueror HTML */
        -moz-user-select: none; /* Old versions of Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
        user-select: none; /* Non-prefixed version, currently supported by Chrome, Edge, Opera and Firefox */
    }
</style>
  