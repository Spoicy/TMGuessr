<script>
  export default {
    
  }
</script>

<template>
  <div class="map-select">
    <div class="map-grid-wrapper">
      <div class="map-grid">
        <div class="map white">1</div>
        <div class="map white">2</div>
        <div class="map white">3</div>
        <div class="map white">4</div>
        <div class="map white">5</div>
        <div class="map green">6</div>
        <div class="map green">7</div>
        <div class="map green">8</div>
        <div class="map green">9</div>
        <div class="map green">10</div>
        <div class="map blue">11</div>
        <div class="map blue">12</div>
        <div class="map blue">13</div>
        <div class="map blue">14</div>
        <div class="map blue">15</div>
        <div class="map red">16</div>
        <div class="map red">17</div>
        <div class="map red">18</div>
        <div class="map red">19</div>
        <div class="map red">20</div>
        <div class="map black">21</div>
        <div class="map black">22</div>
        <div class="map black">23</div>
        <div class="map black">24</div>
        <div class="map black">25</div>
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
      background-color: rgba(200,200,200,0.5);
      border-style: solid;
      border-width: 2px;
      margin: 1px;
      color:black;
      font-weight: 600;
      font-family: Montserrat;
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