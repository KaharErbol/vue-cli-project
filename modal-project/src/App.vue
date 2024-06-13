<template>
  <div class="nav">
    <a @click="signUp">Sign Up</a>
  </div>
  <h1>{{ title }}</h1>
  <input placeholder="email" type="text" ref='name'>
  <button @click="toggleModal">Subscribe</button>
  <teleport to=".modals" v-if="showModal">
    <Modal :header="header" :moto="moto" theme="sale" @close="toggleModal">
      <!-- slot -->
      <h2>This is Slot!</h2>
      <!-- name slot  -->
      <template v-slot:links>
        <a href="#">Send Message</a>
        <a href="#">Sign Up</a>
      </template>
    </Modal>
  </teleport>

  <teleport to=".modals" v-if="showModalTwo">
    <Modal  @close="toggleModalTwo">
      <!-- slot -->
      <h1>Sign up to the newsletter!</h1>
      <p>For updates and promo codes!</p>
    </Modal>
  </teleport>

  <button @click="toggleModalTwo">open modal 2</button>
  <div class="reactionGame">
    <h1>Reaction Timer Game</h1>
    <button class="startBtn" @click="start" :disabled="isPlaying">Play</button>
    <Block v-if="isPlaying" v-bind:delay="delay" @end="endGame"/>
    <Results v-if="showResult" :score="score"/>
  </div>

  <teleport to=".sign" v-if="canSignup">
    <SignupForm />
  </teleport>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Modal from './components/Modal.vue'
import Block from './components/Block.vue'
import Results from './components/Results.vue'
import SignupForm from './components/SignupForm.vue'

export default {
  name: 'App',
  components: { Modal, Block, Results, SignupForm },
  data() {
    return {
      title: 'Beetlia',
      header: 'Sign up for consultation!',
      moto: 'Sunny',
      showModal: false,
      showModalTwo: false,
      isPlaying: false,
      delay: null,
      score: null,
      showResult: false,
      canSignup: false
    }
  },
  methods: {
    signUp() {
      this.canSignup = true
    },
    toggleModal() {
      // console.log(this.$refs.name)
      // this.$refs.name.classList.add('active')
      this.showModal = !this.showModal
    }, 
    toggleModalTwo() {
      this.showModalTwo = !this.showModalTwo
    },
    start () {
      this.showResult = false
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      console.log(this.delay)

    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResult = true
    }
  }
}
</script>

<style>
#app, .modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.nav {
    position: fixed;
    top: 0;
    width: 100%;
    height: 32px;
    background-color: #f8f9fa; /* Light background color for visibility */
    border-bottom: 1px solid #ddd; /* Optional: Adds a border for better separation */
}

.nav a {
    margin: 4px;
    cursor: pointer;
    display: inline-block;
    height: 26px;
    line-height: 16px; /* Aligns text vertically */
    padding: 2px 10px; /* Adds some padding for the button look */
    background-color: #007bff; /* Button background color */
    color: white; /* Button text color */
    text-decoration: none; /* Removes underline from link */
    border-radius: 4px; /* Optional: Adds rounded corners */
    position: absolute;
    right: 10px; /* Adjust spacing from the right edge */
    top: 0; /* Ensures the a tag is aligned at the top */
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box; /* Ensures padding is included in the height calculation */
}

h1 {
  color: rgb(21, 123, 170);
}

input {
  padding: 8px;
  font-size: 14px;
}

button {
  background-color: rgb(8, 109, 203);
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
