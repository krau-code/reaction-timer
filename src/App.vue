<template>
  <h1>Reaction Timer</h1>
  <p>Click the block as fast as possible when it appears.</p>
  <button @click="start" :disabled="isPlaying">PLAY</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" @tooEarly="clickedEarly" />
  <Results v-if="showResults" :displayScore="score"/>
  <p v-if="showTooEarly" class="too-early">clicked too early, play again</p>
</template>

<script>
import Block from './components/Block.vue';
import Results from './components/Results.vue';

export default {
  name: 'App',
  title: 'Reaction Timer',
  components: {
    Block,
    Results
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      showTooEarly: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000; // between 2 to 7 seconds
      this.isPlaying = true;
      this.showResults = false;
      this.showTooEarly = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults = true;
    },
    clickedEarly() {
      this.isPlaying = false;
      this.showTooEarly = true;
    }
  }
}
</script>

<style>
  #app {
    text-align: center;
    margin-top: 40px;
  }

  p {
    margin: 15px auto 20px auto;
  }

  button {
    font-family: 'Montserrat', sans-serif;
    background: #30E3CA;
    color: #40514E;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin-top: 15px;
    transition: 0.1s ease-in;
  }

  button:hover {
    transform: scale(0.9);
  }

  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }

  button[disabled]:hover {
    transform: none;
  }
  
  .too-early {
    color: #fb6962;
    font-size: 1.2rem;
    margin-top: 50px;
  }
</style>
