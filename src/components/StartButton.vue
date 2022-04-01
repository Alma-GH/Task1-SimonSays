<template>
  <button class="btn" @click="cb">Play</button>
</template>

<script>
export default {
  props:["cb"],
}
</script>

<style scoped>
.btn{
  height: 40px;

  padding: 5px 10px;
  background-color: white;
  border-color: lightgreen;
  border-style: solid;
  border-radius: 5px;
  box-shadow: 4px 4px 1px rgba(0, 0, 0, 0.55);

  color: #78ce78;
}

.btn:active{
  box-shadow: 2px 2px 1px rgba(0, 0, 0, 0.55);
}
.btn:disabled{
  color: grey;
  border-color: grey;
}
</style>