<template>
  <div id="app">
    <h1>Simon Says</h1>
    <SimonGame/>
  </div>
</template>

<script>
import SimonGame from "@/components/SimonGame";
export default {
  components:{
    SimonGame
  },
  name: 'App'
}
</script>

<style>
#app {
  height: 100vh;
  /*background-color: lightgreen;*/
  display: grid;
  place-items: center;
}
#app>h1{
  position: absolute;
  top: 20px;
}
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
