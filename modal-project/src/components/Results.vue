<template>
  <div class="result">
    <p>Reaction time: {{ score }}ms</p>
    <p class="rank">{{ rank }}</p>
  </div>
</template>

<script>
export default {
  props: ['score'],
  data() {
    return {
      rank: null
    }
  },
  mounted() {
    if (this.score < 250) {
      this.rank = 'Cat reaction!'
    } else if (this.score < 400) {
      this.rank = 'Rapid Reflexes'
    } else {
      this.rank = 'Snail pace...'
    }
  }
}
</script>

<style>
  .rank {
    font-size: 1.4em;
    font-weight: bold;
    color: rgb(8, 109, 203);
  }
</style>