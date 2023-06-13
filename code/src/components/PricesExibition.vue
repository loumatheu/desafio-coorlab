<template>
    <div class="price-result">
      <h5 v-if="!cheapest" style="align-self: center; text-align: center;">
        <span>Nenhum dado selecionado</span>
      </h5>
      <h5 v-if="cheapest">
        Estas são as melhores alternativas de frete que encontramos para você:
      </h5>
  
        <TransportInfo
            v-if="cheapest"
            text="Frete com menor valor"
            :data="cheapest"
            color1="#e0e0df"
            color2="#asdf4e"
            icon_path=""
        />
        
      
        <TransportInfo
            v-if="fastest"
            text="Frete mais rápido"
            :data="fastest"
            color1="#efeff2"
            color2="#95b4c7"
            icon_path=""
        />

    </div>
  </template>
  
  <script>
  import TransportInfo from './TransportInfo.vue';
  
  export default {
    props: {
      cheapest: Object,
      fastest: Object
    },
    components: {
      TransportInfo
    }
  }
  </script>
  
  <style>
    .price-result {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
      height: 40rem;
      padding: 3rem;
      width: 60vw;
      position: relative;
    }

    .icon {
      width: 20px;
      height: 20px;
      margin-right: 10px;
    }

  </style>