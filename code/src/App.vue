<template>
  <div id="app">
    <HeaderTrans />
    <BestTransport/>
  </div>
</template>

<script>
  import HeaderTrans from './components/HeaderTrans.vue';
  import BestTransport from './components/BestTransport.vue'
  //import ContentBox from './components/ContentBox.vue';

  export default {
    name: 'App',
    components: {
      //ContentBox,
      BestTransport,
      HeaderTrans
    }
  }
</script>

<style>
  .app {
    background-color: gray;
    height: 100vh;
  }
</style>
