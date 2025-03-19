<script lang="ts">
  import ColorCell from "./ColorCell.svelte"
  interface P {
    colors: number[],
    isPicker?: boolean
  }
  let {colors=$bindable(), isPicker=false}:P = $props();

  let colorsM:string[] = $state(["grey", "grey", "grey", "grey"]);

</script>

<div class="container">
  <div class="colors">
    {#each [0,1,2,3] as index}
      <ColorCell bind:colorNumber={colors[index]} {isPicker}/>
    {/each}
  </div>
</div>

<style>
  .container{
    width: 300px;

  }
  .colors{
    min-width: 250px;
    height: 100px;
    /* display: flex; */
    /* flex-direction: row; */
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    align-items:center;
    gap: 5px;
    padding: 0px 10px;
  }

</style>