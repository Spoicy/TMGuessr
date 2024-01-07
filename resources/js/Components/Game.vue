<script>
  import MapSelect from '@/Components/MapSelect.vue';
  import Results from '@/Components/Results.vue';
  import GameResults from '@/Components/GameResults.vue';

  export default {
    props: ['mode', 'game', 'campaign'],
    components: {
      MapSelect, Results, GameResults
    },
    data() {
      return {
        isOngoing: true,
        state: 'select',
        mapPool: [9, 4, 3, 1, 7],
        currentMap: 0,
        submittedAnswer: 0,
        pointsAwarded: [],
        totalPoints: 0,
        calculatedPoints: 0,
        timerEnabled: true,
        timerCount: 0,
        scorePercentage: 100
      }
    },
    methods: {
      processAnswer(answer) {
        this.timerEnabled = false;
        this.submittedAnswer = answer;
        this.calculateResults();
        this.state = 'results';
      },
      calculateResults() {
        var bottomOfColor = Math.floor(this.mapPool[this.currentMap] / 5) * 5 + 1;
        var topOfColor = Math.ceil(this.mapPool[this.currentMap] / 5) * 5;
        if (bottomOfColor <= this.submittedAnswer && this.submittedAnswer <= topOfColor) {
          this.calculatedPoints += 1000;
          this.calculatedPoints += 1000 * (4 - Math.abs(this.mapPool[this.currentMap] - this.submittedAnswer));
          this.calculatedPoints = Math.round(this.calculatedPoints * (this.scorePercentage / 100));
        } else {
          this.calculatedPoints = 0;
        }
        this.pointsAwarded.push(this.calculatedPoints);
        this.totalPoints += this.calculatedPoints;
      },
      loadNext() {
        this.scorePercentage = 100;
        this.timerCount = 0;
        this.currentMap++;
        if (this.currentMap >= this.mapPool.length) {
          this.isOngoing = false;
        } else {
          this.state = 'select';
          this.timerEnabled = true;
          this.calculatedPoints = 0;
          this.submittedAnswer = 0;
        }
      },
      finishGame() {
        this.$emit('gameFinished');
      }
    },
    watch: {
      timerCount: {
        handler(value) {
          if (this.timerEnabled) {
            setTimeout(() => {
              this.timerCount++;
              if (this.timerCount >= 50 && this.timerCount % 10 === 0 && this.scorePercentage > 10) {
                this.scorePercentage--;
              }
            }, 100)
          }
        },
        immediate: true
      }
    },
  }
</script>

<template>
  <div class="game">
    <div class="image-display"></div>
    <MapSelect v-show="state === 'select'" @answerSubmitted="processAnswer" />
    <Results :totalPoints="totalPoints" :awardedPoints="calculatedPoints" :correctAnswer="mapPool[currentMap]" 
      :submittedAnswer="submittedAnswer" :final="currentMap >= 4" v-if="state === 'results' && isOngoing" @nextPressed="loadNext" />
    <GameResults :points="pointsAwarded" :maps="mapPool" :totalPoints="totalPoints" v-if="!isOngoing" @donePressed="finishGame" />
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