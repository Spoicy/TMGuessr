<script>
import PageLayout from '@/Layouts/PageLayout.vue';
import { Head } from '@inertiajs/vue3';
import GameSelect from '@/Components/GameSelect.vue';
import Game from '@/Components/Game.vue';

export default {
  components: {
    GameSelect, PageLayout, Head, Game
  },
  data() {
    return {
      selectedMode: 'casual',
      selectedGame: '',
      selectedCampaign: '',
      shared: false,
      gameOngoing: false,
      activeNav: 'home'
    }
  },
  methods: {
    updateMode(value) {
      this.selectedMode = value;
    },
    updateGame(value) {
      this.selectedGame = value;
      console.log('game updated in homeview to ' + value);
    },
    gameStart(game, campaign, shared) {
      this.selectedGame = game;
      this.selectedCampaign = campaign;
      this.shared = shared;
      this.gameOngoing = true;
      this.$emit('gameStart');
    },
    resetGame() {
      this.gameOngoing = false;
      this.selectedGame = '';
      this.selectedCampaign = '';
    }
  },
};
</script>

<template>
  <Head title="Play" />

  <PageLayout :active="activeNav">
    <main v-if="!gameOngoing">
      <h1>Select a mode</h1>
      <GameSelect :selectedMode="selectedMode" @modeUpdate="updateMode" @gameUpdate="updateGame" @gameStart="gameStart"/>
    </main>
    <main v-else>
      <Game :mode="selectedMode" :game="selectedGame" :campaign="selectedCampaign" @gameFinished="resetGame" />
    </main>
  </PageLayout>
</template>

<style>
  main {
    display: flex;
    flex-direction: column;
  }
</style>