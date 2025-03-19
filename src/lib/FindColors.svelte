<script lang="ts">
  import GuessColors from "$lib/components/GuessColors.svelte"
  import ColorControl from "$lib/components/ColorControl.svelte"

  interface P {
    colors:number[],
    control: number[]
  }
  let data : P[] = [
    {colors:[5,1,2,3], control:[2,1,1,0]}
  ];
  let attempt = $state([0,0,0,0]);
</script>

<div class="container">
  {#each data as oneData}
  <div class="oneGuess">
    <GuessColors colors={oneData["colors"]}/>
    <ColorControl control={oneData["control"]}/>
  </div>
  {/each}
  <div class="oneGuess">
    <GuessColors colors={attempt} isPicker={true}/>
    <button>Valider</button>
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