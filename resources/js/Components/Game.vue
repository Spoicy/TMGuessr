<script>
  import MapSelect from '@/Components/MapSelect.vue';
  import Results from '@/Components/Results.vue';

  export default {
    props: ['mode', 'game', 'campaign'],
    components: {
      MapSelect, Results
    },
    data() {
      return {
        state: 'select',
        currentMap: 9,
        submittedAnswer: 0,
        totalPoints: 500,
        calculatedPoints: 500
      }
    },
    methods: {
      processAnswer(answer) {
        this.submittedAnswer = answer;
        this.state = 'results';
      },
      loadNext() {
        this.state = 'select';
      }
    },
  }
</script>

<template>
  <div class="game">
    <div class="image-display"></div>
    <MapSelect v-show="state === 'select'" @answerSubmitted="processAnswer" />
    <Results :totalPoints="totalPoints" :awardedPoints="calculatedPoints" v-if="state === 'results'" @nextPressed="loadNext" />
  </div>
</template>

<style lang="scss" scoped>
  .game .image-display {
    position: absolute;
    // TODO: These values are hardcoded. Make them not hardcoded by having the header/footer heights available as a css variable.
    top: 100px;
    bottom: 46px;
    left: 0px;
    right: 0px;
    background: url("/img/Trackmania2023-5-5-19-44-44.jpg") center center / cover no-repeat;
  }
</style>