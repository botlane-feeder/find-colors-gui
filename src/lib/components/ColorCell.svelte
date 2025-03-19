<script lang="ts">
  import ColorPicker from "./ColorPicker.svelte"

  let {colorNumber=$bindable(), isPicker}:{colorNumber:number, isPicker:boolean} = $props();

  let colorData = ["grey", "red", "green", "blue", "yellow", "magenta", "orange"];
  let colorPickerShown=$state(false);

  function selectColor(){
    // Ouvre le colorpicker
    colorPickerShown=!colorPickerShown;
  }
</script>


<div class="container">
  <!-- svelte-ignore a11y_click_events_have_key_events-->
  <div class="cell" class:isPicker onclick={selectColor} tabindex="0" role="button" style="background-color : {colorData[colorNumber]};"></div>

  {#if colorPickerShown && isPicker}
  <div class="picker"><ColorPicker bind:show={colorPickerShown} bind:colorNumber={colorNumber} {colorData}/>  </div>
  {/if}
</div>

<style>
  .container{
    position: relative;
    display : inline-block;
  }
  .cell{
    width: 50px;
    height: 50px;
    border-radius: 50px;
    border: grey solid 1px;
    background-color: white;
    
    transition: all 0.2s ease;
  }
  .isPicker{
    cursor: pointer;
  }
  .isPicker:hover{
    scale:1.2;
  }
  
  .picker{
    position: absolute;
  }

</style>