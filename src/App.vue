<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  
  <Results v-if="showResults" :score='score'/>
</template>

<script>
import Block from "./components/Block.vue";
import Results from './components/Results.vue';
export default {
  name: "App",
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
    };
  },
  methods: {
    start() {
      this.showResults=false;
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      console.log(this.delay);
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults=true;
      this.$emit('result',this.score,this.showResults);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
        border: none;
        display: block;
        text-align: center;
        cursor: pointer;
        text-transform: uppercase;
        outline: none;
        overflow: hidden;
        position: relative;
        color: #eeeeee;
        font-weight: 600;
        font-size: 15px;
        background-color: #3fb1d4;
        padding: 15px 50px;
        margin: 10px auto;
      }
      button[disabled] {
        opacity: 0.2;
        cursor:not-allowed;
      }
</style>
