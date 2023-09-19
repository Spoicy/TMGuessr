<script>
import MapsetOptionsSelect from '@/Components/MapsetOptionsSelect.vue';

export default {
  components: {
    MapsetOptionsSelect,
  },
  props: ['selectedMode'],
  data() {
    return {
      selectState: 'game',
      selectedGame: '',
      selectedCampaign: '',
      gameOptions: ['tm2020', 'tmwt', 'totd', 'other'],
      tm2020Options: ['summer2023', 'spring2023'],
      tmwtOptions: ['2023stage1', '2023stage2', '2023wc'],
      totdOptions: ['2020totd', '2021totd', '2022totd', 'alltotd'],
      otherOptions: ['tmnf', 'tm2stadium', 'tm2canyon', 'tm2valley', 'tm2lagoon', 'tmturbo'],
      sharelinkChecked: false,
      sharelink: 'placeholder'
    }
  },
  methods: {
    updateMode(value) {
      this.$emit('modeUpdate', value);
    },
    gameSelect(value) {
      this.selectedGame = value;
      this.$emit('gameUpdate', value);
      this.stateUpdate('campaign');
    },
    campaignSelect(value) {
      this.selectedCampaign = value;
      this.stateUpdate('settings');
    },
    stateUpdate(value) {
      this.selectState = value;
    },
    gameStart() {
      this.$emit('gameStart', this.selectState, this.selectedGame, this.selectedCampaign, this.sharelinkChecked);
    }
  },
}
</script>

<template>
  <div class="game-select">
    <div class="mode-select">
      <button :class="'btn-mode' + (selectedMode === 'casual' ? ' active' : '')" @click="updateMode('casual')">
        <span>Casual Run</span>
      </button>
      <button :class="'btn-mode' + (selectedMode === 'challenge' ? ' active' : '')" @click="updateMode('challenge')">
        <span>Challenge Run</span>
      </button>
    </div>
    <div class="mapset-grid-wrapper" v-show="selectState === 'game'">
      <MapsetOptionsSelect :options="gameOptions" id="gameselect" type="game" @gameSelect="gameSelect" />
    </div>
    <div class="mapset-grid-wrapper" v-show="selectState === 'campaign'">
      <MapsetOptionsSelect v-show="selectedGame === 'tm2020'" :options="tm2020Options" id="tm2020select" type="campaign"
        @campaignSelect="campaignSelect" />
      <MapsetOptionsSelect v-show="selectedGame === 'tmwt'" :options="tmwtOptions" id="tmwtselect" type="campaign"
        @campaignSelect="campaignSelect" />
      <MapsetOptionsSelect v-show="selectedGame === 'totd'" :options="totdOptions" id="totdselect" type="campaign"
        @campaignSelect="campaignSelect" />
      <MapsetOptionsSelect v-show="selectedGame === 'other'" :options="otherOptions" id="otherselect" type="campaign"
        @campaignSelect="campaignSelect" />
    </div>
    <div class="settings-wrapper" v-show="selectState === 'settings'">
      <h2>Settings</h2>
      <div class="setting" v-if="selectedMode === 'challenge'">
        <label for="timelimit">Time limit</label>
        <input type="number" name="timelimit" id="timelimit" min="10" max="120" value="60" />
      </div>
      <div class="setting">
        <label for="sharelinkbox">Enable shareable link
          <sup class="info-popup" data-toggle="tooltip"
            title="Enabling this will prevent scores from being uploaded to leaderboards.">
            <i class="bi bi-info-circle-fill"></i>
          </sup>
        </label>
        <input type="checkbox" v-model="sharelinkChecked" name="sharelinkbox" id="sharelinkbox">
      </div>
      <div class="setting" v-if="sharelinkChecked">
        <label for="sharelink">Shareable link</label>
        <input type="text" name="sharelink" id="sharelink" v-model="sharelink" disabled>
        <button class="copylink-btn" id="copylink">Copy</button>
      </div>
      <div class="start-game">
        <button class="green-accent" id="start" @click="gameStart">Start Game</button>
      </div>
    </div>
    <div class="kofi" v-if="false">
      <p>Support us and the servers on <a href="#">Ko-fi</a>! ☕</p>
    </div>
  </div>
</template>

<style lang="scss">
.settings-wrapper input {
  font-family: 'Montserrat';
  padding: 1px 4px;
  color: #000;
}

.game-select {
  width: min(800px, 100vw - 6rem);
  margin: 3rem auto;
  background-color: #0A3B6C;
  flex: 1;
  display: flex;
  flex-direction: column;

  h2 {
    text-align: center;
  }

  .mapset-grid-wrapper,
  .settings-wrapper {
    flex: 1;
  }

  .kofi {
    text-align: center;
    font-weight: 500;
    margin-bottom: 0.5rem;

    a {
      color: #6efaa0;
    }
  }

  .mode-select {
    display: grid;
    grid-template-columns: 1fr 1fr;

    .btn-mode {
      padding: 0.75rem;
      display: flex;
      justify-content: center;
    }

    .btn-mode {
      font-family: Montserrat;
      font-weight: 500;
      font-size: 1.5rem;
      border: none;
      background-color: rgba(0, 0, 0, 0.1);
      color: white;
      position: relative;
      transition: all 0.5s;
    }

    .btn-mode:hover {
      cursor: pointer;
    }

    .btn-mode:hover,
    .btn-mode.active {
      background-color: rgba(0, 0, 0, 0.25);
      color: #6efaa0;
    }

    .btn-mode span::after {
      content: '';
      position: absolute;
      bottom: -2px;
      left: 0;
      width: calc(100%);
      background-color: #6efaa0;
      opacity: 1;
      height: 0.125em;
    }

    .btn-mode:not(.active) span::after {
      transition: all 300ms;
      transform: scale(0);
      transform-origin: center;
      background-color: white;
    }

    .btn-mode:not(.active):hover span::after,
    .btn-mode:not(.active):focus span::after {
      transform: scale(1);
      background-color: #6efaa0;
    }
  }

  .settings-wrapper {
    text-align: center;
    padding: 2rem;

    .setting {
      margin-top: 1rem;
      margin-bottom: 1rem;
    }

    h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
    }

    label {
      margin-right: 0.5rem;
    }

    .copylink-btn {
      margin-left: 0.25rem;
    }

    .start-game button {
      font-size: 2rem;
      padding: 0.5rem 1rem;
      font-family: 'Montserrat';
      font-weight: 700;
      border-radius: 0.5rem;
    }
  }
}</style>