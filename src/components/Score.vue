<template>
<div id="score">
    {{correct}} Correct / 
    {{attempted}} Attempted
</div>
</template>

<script>
export default {
  name: 'Score',
  props: {
    correct: Number,
    attempted: Number
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>