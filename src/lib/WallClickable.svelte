<script>
    import parchment from "../assets/Parchment.png";
    import FingerPrint from "./FingerPrint.svelte";

    let text="If this notes here, Im in distress!  Find the stone that you must press!";
    let fingerprintArray = [];
    const onWallClick = (e) => {
        let xPos = e.pageX;
        let yPos = e.pageY;

        fingerprintArray = fingerprintArray.concat({xPos: xPos, yPos: yPos});

        text="";

        if(xPos < 100){
            text = text + "The stones quite far ";
        }else if(xPos < 200){
            text = text + "A great deal right ";
        }else if(xPos < 300){
            text = text + "Step to the right ";
        }else if(xPos < 400){
            text = text + "Move to the right ";
        }else if(xPos < 500){
            text = text + "A little right ";
        }else if(xPos < 620){
            text = text + "A tidbit right ";
        }else if (xPos < 700){
            text = text + "A tidbit left ";
        }else if (xPos < 800){
            text = text + "A little left ";
        }else if (xPos < 900){
            text = text + "Move to the left ";
        }else if (xPos < 1000){
            text = text + "Step to the left ";
        }else if (xPos < 1100){
            text = text + "A great deal left ";
        }else {
            text = text + "The stones quite far ";
        }

        if(yPos < 248){
            text = text + "and down some more to find Telemys magic door!";
        }else{
            text = text + "and up a bit to find the stone that you must hit!";
        }
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="wall-clickable" on:click={(e)=>{onWallClick(e)}}>
    {#each fingerprintArray as fingerprint}
        <FingerPrint X={fingerprint.xPos} Y={fingerprint.yPos}/>
    {/each}
    <div class="wall-text-bubble">
        <img src={parchment} alt="parchment-background" class="parchment-img"/>
        <span class="parchment-text">{text ? text : ""}</span>
    </div>
</div>

<style>
    .wall-clickable{
        position: absolute;
        display: flex;

        justify-content: center;

        height: 100vh;
        width: 100vw;

        padding: 0px;
        margin: 0px;
        
        top: 0px;
        left: 0px;
    }

    .wall-text-bubble{
        display: flex;
        flex-direction: column;
        align-items: center;

        text-align: center;
        vertical-align: middle;

        margin-top: 25px;

        width: fit-content;
        height: fit-content;

        text-align: center;
        vertical-align: middle;
    }
    
    .parchment-img{
        width: 200px;
    }

    .parchment-text{
        position: absolute;
        height: 135px;
        width: 160px;

        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
  