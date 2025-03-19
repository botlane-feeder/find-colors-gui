<script lang="ts">
  import GuessColors from "$lib/components/GuessColors.svelte"
  import ColorControl from "$lib/components/ColorControl.svelte"

  interface P {
    attemptStack : { colors:number[], control: number[] }[],
    attempt : number[],
    verify: boolean
  }
  let {attemptStack=$bindable(), attempt=$bindable(), verify=$bindable()}:P = $props();
  let isComplete = $derived( attempt.every((element)=>{return element != 0}) );

</script>

<div class="container">
  {#each attemptStack as oneAttempt}
  <div class="oneGuess">
    <GuessColors colors={oneAttempt["colors"]}/>
    <ColorControl control={oneAttempt["control"]}/>
  </div>
  {/each}
  <div class="oneGuess">
    <GuessColors bind:colors={attempt} isPicker={true}/>
    <button onclick={()=>{verify=true;}} disabled={!isComplete}>Valider</button>
  </div>
</div>

<style>
  .container{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .oneGuess{
    border: black solid 1px;
    padding: 10px;
    min-width: 600px;

    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
</style>