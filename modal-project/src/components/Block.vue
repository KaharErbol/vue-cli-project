<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
    click me
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0
    }
  },
  // hooks
  mounted() {
    console.log('mounted!')
    setTimeout(() => {
      this.showBlock = true
      console.log(this.delay)
      this.startTimer()
    }, this.delay) 
  },
  updated() {
    console.log("Component Updated!")
  },
  unmounted() {
    console.log("Unmounted")
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      console.log('Reaction time:', this.reactionTime)
      this.$emit('end', this.reactionTime)
    }
  }
}
</script>

<style>
  .block {
    width: 400px;
    border-radius: 20px;
    background: black;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
  }
</style>