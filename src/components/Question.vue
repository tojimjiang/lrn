<template>
<div>
    <h1 id='prompt'>{{values[0]}} {{op?"+":"*"}} {{values[1]}}</h1>
    <form v-on:submit.prevent="test">
    <input id='answer' type='text' v-model='answer' />
    <button > ❯ </button>
    </form>
    </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    values: Array,
    op: Number
  },
  data: function () {
        return {
            answer: ""
        }
    },
  methods: {
    test(event) {
      if (this.answer) {
        let parsed = parseInt(this.answer);
        if (!isNaN(parsed)) {
          if (this.op == 1 && this.values[0] + this.values[1] == parsed) {
            this.$emit("correctE", {})
            this.answer = "";
            event.preventDefault();
          }
          else if (this.op == 0 && this.values[0] * this.values[1] == parsed) {
            this.$emit("correctE", {});
            this.answer = "";
            event.preventDefault();
          } 
          else {
            this.$emit("wrongE", {});
            this.answer = "";
            event.preventDefault();
          }
        } else {
          this.$emit("wrongE", {});
          this.answer = "";
          event.preventDefault();
        }
      } else {
        this.$emit("wrongE", {});
        this.answer = "";
        event.preventDefault();
      }
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>