<template>
  <div class="flex">

    <div class="box"
    :style="{'background-color':color1}"
    style="width: 21vw;">
      <a style="font-weight: bold;">{{ text }}</a>
      <a>Transportadora: {{ data.name }}</a>
      <a>Tempo estimado: {{ data.lead_time }}</a>
    </div>

    <div class="box"
    :style="{'background-color':color1}"
    style="width: 12vw; margin-left: .7rem;">
      <a style="font-weight: bold;">Preço:</a>
      <a>{{ data.cost.toLocaleString('pt-br',{style: 'currency', currency: 'BRL'}) }}</a>
    </div>

  </div>
  </template>
  
<script>
  export default {
    props: {
      text: String,
      data: Object,
      color1: String,
      color2: String,
      icon_path: String
    }
}
</script>

<style>
  .box {
    min-height: 6rem;
    margin-top: 1rem;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    padding: .6rem;
    justify-content: center;
  }
  .flex {
    display: flex;
  }


</style>