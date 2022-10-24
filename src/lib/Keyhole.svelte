<script>
    import jingleJangle from "../assets/jingle-jangle.png";
    import keyhole from "../assets/keyhole.svg";
    import parchment from "../assets/Parchment.png";
</script>

<div class="keyhole-container">
    <img src={jingleJangle} alt="Jingle Jangle" class="jingle-img"/>
    <div class="wall-text-bubble">
        <img src={parchment} alt="parchment-background" class="parchment-img"/>
        <span class="parchment-text">I see youve passed Telemys test. Come to my foyer, take a rest.</span>
      </div>
    <img src={keyhole} alt="Keyhole" class="keyhole-img"/>
</div>
    
<style>
    .keyhole-container{
        overflow: hidden;
    }

    .keyhole-img{
        position: absolute;
        top: calc(50vh - 50px);
        left: calc(50vw - 10px);
        animation: grow-huge 5s cubic-bezier(.81,.26,.77,.77) 10s 1 normal both;
        overflow: hidden;
    }

    .jingle-img{
        height: 50vh;
        position: absolute;
        bottom: 0px;
        animation: walk 3s ease-in-out 0s 1 normal both,
        hop 0.5s ease-in-out 0.5s 5 normal backwards  ;
    }

    .wall-text-bubble{
        position: absolute;
        top: calc(50vh - 115px);
        left: calc(50vw - 150px);

        display: flex;
        flex-direction: column;
        align-items: center;

        text-align: center;
        vertical-align: middle;

        width: fit-content;
        height: fit-content;

        text-align: center;
        vertical-align: middle;

        animation: fade-in 3s ease-in-out 3s 1 normal both;
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

        padding-top:0px;
    }

    @keyframes walk{
        from{
            left: calc(-465px);
        }
        to{
            left: calc(50vw - 232px);
        }
    }
    @keyframes hop{
        from{
            bottom: 0px;
        }
        to{
            bottom: 10px;
        }
    }

    @keyframes fade-in{
        from{
            opacity: 0%;
        }
        to{
            bottom: 100%;
        }
    }

    @keyframes grow-huge{
        from{
            top: calc(50vh - 50px);
            left: calc(50vw - 10px);
            width: 0vw;
        }
        to{
            top: calc(-200vh);
            left: calc(-50vw);

            width: 200vw;
        }
    }
</style>