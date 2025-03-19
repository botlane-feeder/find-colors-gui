<script lang="ts">

  let {control}: {control:number[]} = $props();
  let colorsData=["white", "grey", "black"];

</script>

<div class="container">
  {#each control as control}
  <div class="ballControl" style="background-color : {colorsData[control]};"></div>
  {/each}
</div>

<style>
  .container{
    /* border: grey solid 1px; */
    display: grid;
    grid-template-columns: repeat(2,1fr);
    align-items: center;
    gap: 0px;
    height: 50px;
  }
  .ballControl{
    width: 20px;
    height: 20px;
    border-radius: 20px;
    border: grey 1px solid;
  }

</style>