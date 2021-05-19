<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Question v-bind:values="values" v-bind:op="op" v-on:correctE="correctEvent" v-on:wrongE="wrongEvent"/>
    <Score v-bind:correct="correct" v-bind:attempted="attempted" />
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Score from './components/Score.vue'

export default {
  name: 'App',
  components: {
    Question,
    Score
  },
  data: function () {
    return {
      values: this.newValues(),
      op: this.newOp(),
      correct: 0,
      attempted: 0
    }
  },
  methods: {
    correctEvent() {
        this.correct++;
        this.attempted++;
        this.values = this.newValues();
        this.op = this.newOp();
    },
    wrongEvent() {
        this.attempted++;
        this.values = this.newValues();
        this.op = this.newOp();
    },
    newValues() {
      return [Math.floor(Math.random()*10), Math.floor(Math.random()*10)];
    },
    newOp() {
      return Math.floor(Math.random()*2);
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
