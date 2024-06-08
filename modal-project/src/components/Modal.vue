<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal" :class="{sale: theme === 'sale'}">
      <h1>{{ moto }}</h1>
      <h3>Now the dark days are done</h3>
      <h3>And the bright days are here</h3>
      <p>{{ header }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['header', 'moto', 'theme'],
  methods: {
    closeModal() {
      this.$emit('close')
    }
  }
}
</script>


<style scoped>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
  }
  .backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
  }
  h1, h3 {
    color: rgb(208, 147, 6);
  }

  .modal.sale {
    background: crimson;
    color: white;
  }

  .modal.sale h1{
    color: white;
  }
</style>