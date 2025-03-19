<script lang="ts">
  interface P {
    show:boolean,
    colorNumber:number,
    colorData:string[]
  }
  let {show=$bindable(), colorNumber=$bindable(), colorData}:P = $props();

  function selectColor(oneColor:number){
    colorNumber = oneColor;
    show=false;
  }

</script>

<div class="container">
  {#each colorData as oneColor, index}
    {#if index != 0}
      <!-- svelte-ignore a11y_click_events_have_key_events a11y_no_static_element_interactions -->
      <div class="circleColor" style="background-color: {oneColor}" onclick={()=>{selectColor(index)}} tabindex="0" role="button"></div>
    {/if}
  {/each}
</div>

<style>
  .container{
    border: solid 1px grey;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    padding : 10px 10px;
    background-color: #FFFFFF;
  }

  .circleColor{
    width: 40px;
    height: 40px;
    border-radius: 40px;

    cursor: pointer;
  }
</style>