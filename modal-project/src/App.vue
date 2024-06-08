<template>
  <h1>{{ title }}</h1>
  <input placeholder="email" type="text" ref='name'>
  <button @click="toggleModal">Subscribe</button>
  <div v-if="showModal">
    <Modal :header="header" :moto="moto" theme="sale" @close="toggleModal"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: { Modal },
  data() {
    return {
      title: 'Beetlia',
      header: 'Sign up for consultation!',
      moto: 'Sunny',
      showModal: false
    }
  },
  methods: {
    toggleModal() {
      // console.log(this.$refs.name)
      // this.$refs.name.classList.add('active')
      this.showModal = !this.showModal
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  color: rgb(21, 123, 170);
}
</style>
