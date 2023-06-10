<template>
  <main class="content p-5 bg-light">
    <div class="title bg-info p-2 rounded-top">Melhor Frete
    </div>
    <div class="content bg-white p-2 pt-4 px-2">
      <div>
        <main>
          <div>
            <h3>Insira o destino e o peso</h3>
          </div>
          <div class="d-flex">
            <div class="w-25">
              <form class="form">
                <div class="form-group">
                  <label for="destino">Destino</label>
                  <input class="form-control" type="text" name="destino">
                </div>
                <div class="form-group">
                  <label for="peso">Peso</label>
                  <input class="form-control" type="text" name="peso">
                </div>
                <button class="mt-4 btn-info border-0 rounded" type="submit">Analisar</button>
              </form>
            </div>
            <div class="w-75">
              <h5 class="text-center">Nenhum dado selecionado.</h5>
            </div>
          </div>
        </main>
      </div>
    </div>
  </main>
 
</template>

<script>

export default {
  components: {
    
  },
  data() {
    const appName = ''

    return {
      appName,
    }
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = 'Melhor Frete'
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
    methodFoo() {
      console.log(this.appName)
    },
  },
}
</script>

<style scoped>
.title .navbar {
  background-color: #00aca6 !important;
}

.title .navbar-brand {
  margin-left: 20px;
}

body > div > div > div > div {
  background: #000;
}

</style>
