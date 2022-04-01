<template>
  <div class="info">
    <h2 v-if="!wait">Memorize</h2>
    <h2 v-else>Go</h2>
    <div class="roundTable">
      Round {{round}}
    </div>
  </div>
</template>

<script>
export default {
  props:["round", "wait"]
}
</script>

<style scoped>
  .info{
    position: absolute;
    top: 0;
    right: 0;
    width: 35%;
    text-align: center;

    padding-top: 10px;
  }
  .info h2{
    margin-bottom: 10px;
  }


</style>