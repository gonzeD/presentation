<script lang="ts">
  import Background from "./background.svelte"
</script>


<style>
  .Card 
  {
    margin : auto;
    background-color: #121212;
    padding : 50px;
    border : 1px solid #1A1A1A;
    border-radius : 4px;
    width : 600px;
    position: relative;
    min-height: 600px;
  }
</style>


<Background/>
<div class="Card">
  <slot/>
</div>