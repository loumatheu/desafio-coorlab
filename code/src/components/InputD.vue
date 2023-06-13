<template>
  <div class="destination">  
    <h3>
      <img src="../assets/mapa.png" alt="Mapa">
      <a>Insira o destino e o peso</a>
    </h3>
      
    <b-form @submit="onSubmit" ref="formRef">
      <b-form-group id="input-group1" label="Destino" label-for="input-1">
        <b-form-select
          id="input-1"
          v-model="form.destination"
          :options="[ { text: 'Selecione o destino', value: null }, ...destinations ]"
          class="form-select"
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Peso" label-for="input-2" class="mt-4">
        <b-form-input
          id="input-2"
          type="number"
          v-model="form.weight"
          placeholder="Peso da carga em kg"
        ></b-form-input>
      </b-form-group>

      <button class="mt-4 custom-button border-0 rounded" type="submit">Analisar</button>
    </b-form>
    <ModalWarning :showModal="showModal" :message="modalMessage" @close="() => showModal=false" />        
  </div>
</template>

<script>
import ModalWarning from './ModalWarning.vue';

    export default {
    props: {
        cidades: Array
    },
    data() {
        return {
            form: {
                weight: null
            },
            showModal: false,
            modalMessage: "",
        };
    },

    computed: {
        destinations() {
            return this.cidades;
        }
    },
    methods: {
        onSubmit(event) {
            event.preventDefault()
            if(!this.form.weight || !this.form.destination) {
              this.modalMessage = 'Insira os valores para realizar a análise.';
              this.showModal = true;
            } else {
              this.$emit("formResponse", this.form);
            }
            
        },
        resetForm() {
            this.$refs.formRef.reset();
        }
    },
    components: { ModalWarning }
}
</script>

<style>
  .custom-button {
    background-color: #85b8c5;
    width: 285px;
  }

  .destination {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: #DEDEDE;
    border-radius: 10px;
    height: 40rem;
    width: 40vw;
    padding: 1rem;
    margin-bottom: 10px;
  }

  img {
    width: 37px;
    height: auto;
    margin-right: 10px;
  }

</style>