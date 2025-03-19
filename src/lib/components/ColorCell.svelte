<script lang="ts">
  import ColorPicker from "./ColorPicker.svelte"

  let {color=$bindable()}:{color:string} = $props();

  let colorPickerShown=$state(false);

  function selectColor(){
    // Ouvre le colorpicker
    colorPickerShown=!colorPickerShown;
  }
</script>


<div class="container">
  <!-- svelte-ignore a11y_click_events_have_key_events-->
  <div class="cell" onclick={selectColor} tabindex="0" role="button" style="background-color : {color};"></div>

  {#if colorPickerShown}
  <div class="picker"><ColorPicker bind:show={colorPickerShown} bind:color={color}/>  </div>
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
    cursor: pointer;
  }
  
  .cell:hover{
    border: grey solid 3px;
  }
  
  .picker{
    position: absolute;
    /* bottom: -100px; */
    /* right: -100px; */

    /* border: grey solid 1px; */
  }

</style>