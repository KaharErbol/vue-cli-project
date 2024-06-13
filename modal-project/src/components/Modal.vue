<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal" :class="{sale: theme === 'sale'}">
      <h1>{{ moto }}</h1>
      <h3>Now the dark days are done</h3>
      <h3>And the bright days are here</h3>
      <slot>Default Slot Content</slot>
      <div class="actions">
        <slot name="links"></slot>
      </div>
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

// if I use scope in style, it did not render the slot
<style>
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
  .modal h1, h3 {
    color: rgb(208, 147, 6);
  }

  .modal.sale {
    background: crimson;
    color: white;
  }

  .modal.sale h1{
    color: white;
  }

  .modal .actions {
    text-align: center;
    margin: 30px 0 10px 0;
    color: #333;
  }

  .modal .actions a {
    color: #333;
    padding: 8px;
    border: 1px solid #eee;
    border-radius: 4px;
    text-decoration: none;
    margin: 10px;
  }

  .modal.sale .actions {
    color: white;
  }

  .modal.sale .actions a{
  color: white;
  }
</style>