<template>
  <div class="modal-warning" v-show="showModal">
    <div class="darkenbg"></div>
    <div class="modal-w-content">
      <img src="../assets/warning-square.svg"/>
      <p>{{ message }}</p>
      <button class="btn-primary" @click="closeModal">Fechar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    message: String,
    showModal: Boolean
  },
  methods: {
    closeModal() {
      this.$emit('close');
    }
  }
};
</script>

<style>
  .modal-warning {
    position: fixed;
    z-index: 10;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal-warning img{
    margin: 1rem;
  }
  .modal-warning p{
    text-align: center;
    font-size: 20px;
  }
  .darkenbg {
    position: fixed;
    background: black;
    z-index: 9;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    opacity: 0.3;
  }
  .modal-w-content {
    z-index: 11;
    max-width: 40vw;
    border: none;
    border-radius: 20px;
    background: white;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>
