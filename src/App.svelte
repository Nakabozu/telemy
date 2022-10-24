<script>
  // NPM Libraries
  import { onMount } from 'svelte';
  // Components
  import CobblestoneClickable from "./lib/CobblestoneClickable.svelte";
  import FloatingScript from "./lib/FloatingScript.svelte";
  import WallClickable from './lib/WallClickable.svelte';
  import Keyhole from './lib/Keyhole.svelte';
  // Sounds
  import magicSound from "./assets/Magic Sound Effect.mp3";
  import triangleSound from "./assets/Triangle Sound Effect.mp3";
  import fizzleSound from "./assets/Fizzle Sound Effect.mp3";
  import keysSound from "./assets/Keys Jingling Sound Effect.mp3";
  // Images
  import magicLoading from "./assets/transparent-magic.gif";
  import parchment from "./assets/Parchment.png";


  let puzzlePhase = 0;

  const onClickCobblestone = () => {
    playSound(magicSound);
    puzzlePhase = 1;
    setTimeout(()=>{
      puzzlePhase = 2;
    }, 2800);
  }

  const runeLocations = [
    {vw: 11, vh: 74},
    {vw: 50, vh: 10},
    {vw: 89, vh: 85},
    {vw: 25, vh: 25},
    {vw: 74, vh: 30},
  ];

  let correctRuneNumber = 1;
  let arrayOfRunes = [];
  const arrayOfCorrectRunes = [
    {letter: "𖹙", patternNumber: 1, X: runeLocations[0].vw + "vw", Y: runeLocations[0].vh + "vh"},
    {letter: "𖹟", patternNumber: 2, X: runeLocations[1].vw + "vw", Y: runeLocations[1].vh + "vh"},
    {letter: "𖹏", patternNumber: 3, X: runeLocations[2].vw + "vw", Y: runeLocations[2].vh + "vh"},
    {letter: "𖹬", patternNumber: 4, X: runeLocations[3].vw + "vw", Y: runeLocations[3].vh + "vh"},
    {letter: "𖹊", patternNumber: 5, X: runeLocations[4].vw + "vw", Y: runeLocations[4].vh + "vh"},
  ];

  const arrayOfIncorrectRunes = [
    "𖹀","𖹁","𖹂","𖹅","𖹆","𖹇","𖹈","𖹉","𖹌","𖹍","𖹎","𖹐","𖹑",
    "𖹒","𖹓","𖹕","𖹖","𖹗","𖹘","𖹚","𖹛","𖹜","𖹝","𖹠","𖹡","𖹢",
    "𖹣","𖹥","𖹦","𖹧","𖹨","𖹩","𖹭","𖹮","𖹯","𖹰","𖹲","𖹳","𖹴","𖹵",
    "𖹶","𖹸","𖹻","𖹼","𖹽","𖹿","𖺀","𖺄","𖺅","𖺆","𖺉","𖺊","𖺋","𖺌",
    "𖺍","𖺎","𖺐","𖺑","𖺒","𖺙"
  ];


  onMount(async () => {
    for(let i = 0; i < 50; i++){
      const randomRuneIndex = Math.floor(Math.random() * arrayOfIncorrectRunes.length);
      let randomX =  Math.floor(Math.random() * 80)+10;
      let randomY =  Math.floor(Math.random() * 80)+10;

      runeLocations.forEach((runeLocation) => {
        if(
          (randomX > runeLocation.vw - 3 && randomX < runeLocation.vw + 3)
          &&
          (randomY > runeLocation.vh - 3 && randomY < runeLocation.vh + 3)
        ){
          if(randomX%2 === 0){
            randomX-=6;
            randomY+=6;
          }else{
            randomX+=6;
            randomY-=6;
          }
          
          console.log("test");
        }
      });

      arrayOfRunes = arrayOfRunes.concat({
        letter: arrayOfIncorrectRunes[randomRuneIndex], patternNumber: 0, X: randomX+"vw", Y: randomY+"vh"
      })
    }
    arrayOfRunes = arrayOfRunes.concat(arrayOfCorrectRunes);
  })

  const playSound = (url) =>{
    new Audio(url).play();
  }
  
  const onClickRune = (numberToBeCorrect) => {
    console.log("onClickRune called with a value of " + numberToBeCorrect);
    if(puzzlePhase === 2 && correctRuneNumber != -1){
      if(numberToBeCorrect === 3 && correctRuneNumber === 6){
        puzzlePhase = 3;
        correctRuneNumber = -1;
        jingleJangleWelcomesYou();
      }
      else if(numberToBeCorrect === correctRuneNumber){
        playSound(triangleSound);
        correctRuneNumber++;
      }else{
        playSound(fizzleSound);
        correctRuneNumber = 1;
      }
      console.log(numberToBeCorrect + " was triggered.");
    }
  }

  let runeParchmentText="A magic pollen chases you. Telemy won't just let you though. "+
  "You've found my cave atop this hill.  But to get in, you'll need goodwill. "+
  "The magic word makes my door open.  Apologies, the last rune's broken.";

  const jingleJangleWelcomesYou = () => {
    playSound(keysSound);
  }
</script>

<main class="main">
  {#if puzzlePhase === 0}
    <WallClickable/>
    <CobblestoneClickable onClickCobblestone={onClickCobblestone}/>
  {/if}

  {#if puzzlePhase === 1}
    <div class="magical-loading">
      <img src={magicLoading} alt="Loading Runes..."/>
    </div>
  {/if}

  {#if puzzlePhase === 2}
  <div class="wall-text-bubble">
    <img src={parchment} alt="parchment-background" class="parchment-img"/>
    <span class="parchment-text">{runeParchmentText}</span>
  </div>
    {#each arrayOfRunes as rune}
      <FloatingScript 
        letter={rune.letter}
        X={rune.X}
        Y={rune.Y}
        onClickLetter={()=>{onClickRune(rune.patternNumber)}}
        isCorrectRuneNumber={correctRuneNumber === rune.patternNumber}/>
    {:else}
      <FloatingScript
        letter={"Gathering Runes..."}
        X={"50vw"}
        Y={"50vh"}
        onClickLetter={()=>{console.log("Patience is key...")}}
        isCorrectRuneNumber={false}/>
    {/each}
  {/if}

  {#if puzzlePhase === 3}
    <Keyhole />
  {/if}
</main>

<style>
  .main{
    height: 100%;
    width: 100%;
    background-image: url("./assets/mossy-cobble.png");
    overflow: hidden;
  }

  .magical-loading{
    display: flex;

    position: absolute;
    left: calc(50vw - 175px);
    top: calc(50vh - 160px);

    height: min-content;
    width: min-content;
  }

  .wall-text-bubble{
        display: flex;
        flex-direction: column;
        align-items: center;

        text-align: center;
        vertical-align: middle;

        margin-top: 25px;
        margin-left: 25px;

        width: fit-content;
        height: fit-content;

        text-align: center;
        vertical-align: middle;
    }
    
    .parchment-img{
        width: 300px;
    }

    .parchment-text{
        position: absolute;
        height: 135px;
        width: 260px;

        display: flex;
        align-items: center;
        justify-content: center;

        padding-top:35px;
    }
  /* NOTES *
    
    
    UPON ERROR:
    I'm afraid you've chosen wrong.
    I hope your gut is mighty strong...

    UPON COMPLETION:
    A toast to you you who has my favor!
    Did you enjoy the floral flavor?
  /**/
</style>

