<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Header v-bind:range="computedRange" v-bind:op="op" v-on:newRange="newRange" />
    <Question v-bind:values="values" v-bind:op="op" v-on:correctE="correctEvent" v-on:wrongE="wrongEvent"/>
    <Score v-bind:correct="correct" v-bind:attempted="attempted" />
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Score from './components/Score.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    Question,
    Score,
    Header
  },
  props: {
    initalRange: {
      type: Array,
      default: function() {return [0,10]},
    }
  },
  computed: {
    computedRange () {
      return this.range || this.initalRange;
    }
  },
  data: function () {
    return {
      range: null,
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
    newRange(event) {
      this.range = event.newRange;
    },
    newValues() {
      if (!this.computedRange) {
        return [Math.floor(Math.random()*(this.initalRange[1] - this.initalRange[0]) + this.initalRange[0]), Math.floor(Math.random()*(this.initalRange[1] - this.initalRange[0])+ this.initalRange[0])];
    
      }
      return [Math.floor(Math.random()*(this.computedRange[1] - this.computedRange[0]) + this.computedRange[0]), Math.floor(Math.random()*(this.computedRange[1] - this.computedRange[0])+ this.computedRange[0])];
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
  /* margin-top: 60px; */
}
</style>
