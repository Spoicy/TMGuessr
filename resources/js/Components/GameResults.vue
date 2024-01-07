<script>
  export default {
    props: ['maps', 'points', 'totalPoints']
  }
</script>

<template>
  <div class="game-results-container">
    <div class="game-results">
      <h2 class="text-center">Final Results</h2>
      <div class="results-grid">
        <div v-for="i in 5" class="result">
          <div class="result-img"></div>
          <p class="text-center">{{ points[i-1] }}</p>
        </div>
      </div>
      <h3 class="text-center">Final score: {{ totalPoints }}</h3>
      <h3 class="text-center">Your high score: 19000</h3>
      <div class="game-results-controls text-center pb-5">
        <button @click="this.$emit('donePressed')" class="button-done py-2 mt-3 px-4 rounded">Done</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .game-results-container {
    position: relative;
    height: calc(100vh - (100px + 46px));
  }
  .game-results {
    display: flex;
    flex: 1;
    flex-direction: column;
    z-index: 10;
    width: min(60%, 850px);
    height: 70%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate3d(-50%, -50%, 0);
    background-color: rgba(12, 73, 130, 0.8);
    h2 {
      font-size: 2rem;
      margin-top: 0.75rem;
    }
    h3 {
      font-size: 1.25rem;
      margin-top: 0.75rem;
    }
    .results-grid {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 1rem;
      padding: 1rem 1rem 0 1rem;
      .result-img {
        background: url(https://prod.trackmania.core.nadeo.online/storageObjects/35ebeb63-c884-4d1d-ad6e-4ca004e92b1b.jpg) center center / cover no-repeat;
        aspect-ratio: 1;
        width: 100%;
        margin-bottom: 0.5rem;
      }
      p {
        font-size: 1.125rem;
      }
    }
    .button-done {
      background-color: #6efaa0;
      transition: all 0.5s;
      font-size: 1.5rem;
      font-weight: 600;
      &:hover,
      &:focus {
        background-color: #54bf7a;
      }
    }
  }
</style>