<script>
export default {
  props: ['options', 'type', 'id'],
  methods: {
    notifyOptionSelect(type, value) {
      this.$emit(type + 'Select', value);
    }
  },
}
</script>

<template>
  <div class="mapset-grid" :id="id">
    <button v-for="option in options" class="mapset-option" :id="option"
      @click="(['tm2020', 'summer2023', 'spring2023'].includes(option)) ? notifyOptionSelect(type, option) : null">
      <img v-if="['tm2020', 'summer2023', 'spring2023'].includes(option)" :src="'/img/tmguessr_' + option + '.jpg'"
        alt="TODO">
      <img v-else src="/img/tmguessr_comingsoon.jpg" alt="TODO">
    </button>
  </div>
</template>

<style lang="scss" scoped>
  .mapset-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;
    padding: 2rem;
  }

  .mapset-option {
    padding: 0;
    margin: 0;
    border: none;
    border-radius: 1rem;
    overflow: hidden;
    height: calc(100% - 3px);
    cursor: pointer;
    background-color: black;
  }

  .mapset-option img {
    width: 100%;
  }

  #tm2020 {
    background-color: #54BF7A;
  }

  #spring2023 {
    background-color: #914158;
  }

  #summer2023 {
    background-color: #D6C429;
  }
</style>