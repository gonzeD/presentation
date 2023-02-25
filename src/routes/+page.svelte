
<style>
  * 
  {
    color : white;
  }

  img 
  {
    width : 150px;
    height: 150px;
    border-radius : 100%;
    overflow : hidden;
    margin : auto;
  }

  .Btns 
  {
    flex-direction: row;
    justify-content: space-between;
  }

  .Btns a 
  {
    background-color: #222;
    border-radius: 4px;
    max-width: 120px;
    min-width: 120px;
    min-height: 90px;
    text-align: center;
    justify-content: center;
    align-items: center;
    line-height: 1.5;
    transition : .1s all ease-in-out;
    box-shadow : 0 0 6px 0 rgba(0,0,0,0.5);
    font-weight: 600;
    font-size : 1.2rem;
  }
  .Btns a:hover
  {
    background-color: #333;
    box-shadow : 0 0 6px 0 rgba(0,0,0,1);
  }
</style>

<script lang="ts">
  import img from "$lib/temp.jpg"
  import { base } from '$app/paths';
</script>


<h1>Damien Gonze</h1>

<img src={img} alt=""/>

<div class="Btns">
  <a href="{base}/web">Web<br/>dev</a>
  <a href="{base}/games">Game designer</a>
  <a href="{base}/contact">Me<br/>contacter</a>
</div>