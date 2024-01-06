<script>
export default {
  props: ['totalPoints', 'awardedPoints', 'correctAnswer', 'submittedAnswer'],
  methods: {
    getMapNumber(num) {
      if (num < 10) {
        return '0' + num;
      } else {
        return num;
      }
    }
  },
}
</script>

<template>
  <div class="results-container">
    <div class="results">
      <h2 class="text-center">Your Result</h2>
      <div class="answers pb-3">
        <div class="answer" id="answercorrect">
          <div class="answer-img"></div>
          <!--<img src="https://prod.trackmania.core.nadeo.online/storageObjects/35ebeb63-c884-4d1d-ad6e-4ca004e92b1b.jpg" alt="">-->
          <p class="text-center pt-2">Correct answer: {{ getMapNumber(correctAnswer) }}</p>
        </div>
        <div class="answer" id="answeryours">
          <div class="answer-img"></div>
          <!--<img src="https://prod.trackmania.core.nadeo.online/storageObjects/35ebeb63-c884-4d1d-ad6e-4ca004e92b1b.jpg" alt="">-->
          <p class="text-center pt-2">Your answer: {{ getMapNumber(submittedAnswer) }}</p>
        </div>
      </div>
      <div class="points text-center pb-3">
        <p>Points earned: {{ awardedPoints }}</p>
        <p>Total points: {{ totalPoints }}</p>
      </div>
      <div class="results-controls text-center pb-5">
        <button @click="this.$emit('nextPressed')" class="button-next py-2 px-4 rounded">Next</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .results-container {
    position: relative;
    height: calc(100vh - (100px + 46px));
  }
  .results {
    display: flex;
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
    .answers {
      flex: 1;
      display: grid;
      gap: 1.5rem;
      grid-template-columns: repeat(2, 1fr);
      .answer {
        padding: 1.5rem;
        padding-top: 0.875rem;
        font-weight: 600;
      }
      .answer-img {
        background-image: url(https://prod.trackmania.core.nadeo.online/storageObjects/35ebeb63-c884-4d1d-ad6e-4ca004e92b1b.jpg);
        height: 100%;
        background-size: 100%;
        background-repeat: no-repeat;
        background-position: center;
      }
      :first-child.answer {
        
        padding-right: 0;
      }
      :last-child.answer {
        padding-left: 0;
      }
    }
    .points {
      font-weight: 600;
    }
    .button-next {
      background-color: #6efaa0;
      transition: all 0.5s;
      font-size: 1.25rem;
      font-weight: 600;
      &:hover,
      &:focus {
        background-color: #54bf7a;
      }
    }
  }
</style>