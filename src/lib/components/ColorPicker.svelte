<script lang="ts">
  let {show=$bindable(), color=$bindable()}:{show:boolean, color:string} = $props();
  let colors = ["red", "green", "blue", "yellow", "magenta", "orange"];

  function selectColor(oneColor:string){
    color = oneColor;
    show=false;
  }

</script>

<div class="container">
  {#each colors as oneColor}
  <!-- svelte-ignore a11y_click_events_have_key_events a11y_no_static_element_interactions -->
    <div class="circleColor" style="background-color: {oneColor}" onclick={()=>{selectColor(oneColor)}} tabindex="0" role="button"></div>
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