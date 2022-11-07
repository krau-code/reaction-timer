<template>
  <div class="flex">
    <Header />
  
    <section id="content">
      <p>Click the block as fast as possible when it appears.</p>
      <button @click="start" :disabled="isPlaying">PLAY</button>

      <!-- Block -->
      <Block v-if="isPlaying" :delay="delay" @end="endGame" @tooEarly="clickedEarly" />

      <!-- Result -->
      <Results v-if="showResults" :displayScore="score"/>

      <!-- Too Early -->
      <p v-if="showTooEarly" class="too-early">clicked too early, play again</p>
    </section>

    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Block from './components/Block.vue';
import Results from './components/Results.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  title: 'Reaction Timer',
  components: {
    Header,
    Block,
    Results,
    Footer
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
  .flex {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  #content {
    text-align: center;
    padding: 3rem 0;
    flex-grow: 1;
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

  @media (max-width: 481px) {
    #content {
      padding: 2rem 0;
      margin: 0 1rem;
    }
  }
</style>
