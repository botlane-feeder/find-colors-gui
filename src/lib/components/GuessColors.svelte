<script lang="ts">
  import ColorCell from "./ColorCell.svelte"

  let colors:string[] = $state(["grey", "grey", "grey", "grey"]);

</script>

<div class="container">
  <div class="colors">
    {#each [0,1,2,3] as index}
      <ColorCell bind:color={colors[index]}/>
    {/each}
  </div>
</div>

<style>
  .container{
    width: 300px;

  }
  .colors{
    border: black solid 1px;
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