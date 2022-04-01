<template>
  <select class="select" id="difficult" @change="changeDifficult">
    <option value="1" selected disabled>Difficult</option>
    <option value="1">Easy</option>
    <option value="2">Medium</option>
    <option value="3">Hard</option>
  </select>
</template>

<script>
export default {
  props:["onplay", "changeDifficult"]
}
</script>

<style scoped>

.select{

}

</style>