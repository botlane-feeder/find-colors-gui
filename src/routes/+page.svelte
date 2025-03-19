<script lang="ts">
  import FindColors from "$lib/FindColors.svelte"

  let level = "soft"; // Tri le control des couleurs
  // let solution = [3,2,3,1];
  let solution = [3,2,1,5];
  interface P {
    colors:number[],
    control: number[]
  }
  let attemptStack : P[] = $state([
    {colors:[5,1,2,3], control:[2,1,1,0]}
  ]);
  let attempt = $state([0,0,0,0]);
  let verify=$state(false);
  $effect(()=>{
    if(verify){
      verify = false;
      verifyAttempt();
    }
  });

  function verifyAttempt(){
    // Vérifie qu'il n'y pas de 0 dans le tableau attempt
    if( attempt.every((element)=>{return element != 0}) ){
      // Ajout de la tentative et son controle de couleur
      attemptStack.push({colors:{ ...attempt}, control:getControlColor(attempt, solution)});
      attempt=[0,0,0,0];
    }
  }
  // Calcule et renvoie le controle des couleurs
  function getControlColor(attempt:number[], solution:number[]):number[]{
    // Vérifie la couleur aux bons endroits
    let blacks = attempt.reduce((accumulator:number[], current:number, index:number)=>{
      if(solution[index] == current){
        accumulator.push(index)
      }
      return accumulator
    }, [] );
    // Supprime les correspondances, en les remplaçant par 0
    let remainingSolution:number[] = solution.reduce((accumulator:number[], current:number, index:number)=>{
      accumulator.push( blacks.includes(index)?0:current );
      return accumulator;
    }, []);
    // Vérifie les couleurs bonnes mais au mauvais endroit
    let whites = attempt.reduce((accumulator:number[], current:number, index:number)=>{
      if( remainingSolution.includes(current) ){
        accumulator.push(index);
        // Supprime la première correspondance trouvées, en les remplaçant par 0
        remainingSolution[ remainingSolution.findIndex((element)=>{return element==current}) ]=0;
      }
      return accumulator
    }, [] );
    // Construction du controle
    let control:number[]=[];
    for (let index = 0; index < 4; index++) {
      let value:number=0;
      if(blacks.includes(index)){
        value = 2;
      }else if(whites.includes(index)){
        value = 1;
      }
      control.push(value);
    }
    if(level=="hard"){
      control.sort((a,b)=>b-a);
    }
    return control;
  }

</script>

<div class="container">
  <FindColors bind:attemptStack={attemptStack} bind:attempt={attempt} bind:verify={verify}/>
</div>

<style>
  .container{
    width: 60%;
    padding: 0px 20%;

    display: flex;
    flex-direction: row;
    justify-content: center;
  }
</style>