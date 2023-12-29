<script>
  export default {
    methods: {
      getColorClass(index) {
        const colorClasses = ["white", "green", "blue", "red", "black"];
        const colorIndex = Math.floor(index / 5) % colorClasses.length;
        return colorClasses[colorIndex];
      },
      selectMap(map) {
        console.log(map);
      }
    },
  }
</script>

<template>
  <div class="map-select">
    <div class="map-grid-wrapper">
      <div class="map-grid">
        <div v-for="index in 25" :key="index" @click="selectMap(index)" :class="['map', getColorClass(index - 1)]">{{ index }}</div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .map-select {
    position: absolute;
    bottom: calc(46px + 0.5rem);
    right: 0.5rem;
    z-index: 10;
    width: calc(50% - 1rem);
    background-color: red;
  }
  .map-grid-wrapper {
    position: relative;
  }
  .map-grid {
    position: absolute;
    right: 0;
    bottom: 0;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: repeat(5, 1fr);
    .map {
      padding: 1rem;
      text-align: center;
      font-size: 1.5rem;
      background-color: rgba(230,230,230,0.5);
      border-style: solid;
      border-width: 2px;
      margin: 1px;
      color:black;
      font-weight: 600;
      font-family: Montserrat;
      &:hover {
        cursor: pointer;
        background-color: rgba(230,230,230,0.75);
      }
      &.white {
        border-color: white;
      }
      &.green {
        border-color: darkgreen;
      }
      &.blue {
        border-color: blue;
      }
      &.red {
        border-color: darkred;
      }
      &.black {
        border-color: black;
      }
    }
  }
</style>