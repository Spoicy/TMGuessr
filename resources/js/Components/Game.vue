<script>
  import MapSelect from '@/Components/MapSelect.vue';

  export default {
    props: ['mode', 'game', 'campaign'],
    components: {
      MapSelect,
    },
  }
</script>

<template>
  <div class="game">
    <div class="image-display"></div>
    <MapSelect />
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