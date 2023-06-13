<template>
  
  <main class="content p-5 bg-light ">
    <div class="title bg-custom custom-txt alignItems p-2 rounded-top">
      <img src="../assets/logo.png" alt="logo" class="logo">
      Melhor Frete
    </div>
    <div class="content bg-white p-2 pt-4 px-4 center-all">
      <InputD :cidades="cidades" @formResponse=" ((e) => dadosForm = e)" ref="formComponentRef"/>
      <PricesExibition :fastest="getFastest()" :cheapest="getCheapest()"/>
      <button class="clear button-absolute rounded" @click="resetForm">Limpar</button>
      </div>
      
  </main>
  
</template>

<script>
import axios from 'axios'
import InputD from './InputD.vue'
import PricesExibition from './PricesExibition.vue'


export default {
  components: {
    InputD,
    PricesExibition
  },
  data() {
    
    let transportData = []
    let cidades = []
    let dadosForm = null;

    return {
      transportData,
      cidades,
      dadosForm
    }
  },
  created() {
    axios.get('http://api.localhost:3000/transport')
      .then(response => {
        this.transportData = response.data;
        this.cidades = this.getcidades(response.data);
      })
       .catch(error => {
        console.error(error); 
       })
  },
  methods: {

    resetForm() {
      this.$refs.formComponentRef.resetForm();
      this.dadosForm = null;
    },

    getcidades(arrayOfTransport) {
      let cidades_arr = [];

      arrayOfTransport.forEach(elem => {
        if (!cidades_arr.includes(elem.city)) {
          cidades_arr.push(elem.city);
        }
      })
      return cidades_arr;
    },

    getCheapest() {
      try {
        if (!this.dadosForm) return null;

        const destination = this.dadosForm.destination
        const weight = this.dadosForm.weight
        let res = {};
        let cheapest = Infinity;

        if (weight > 100) {
          this.transportData.forEach(elem => {
            const cost_heavy = parseFloat(elem.cost_transport_heavy.replace(/[^\d.]/g, ''))
            if (cost_heavy < cheapest && elem.city === destination) {
              cheapest = cost_heavy;
              res = elem;
            }
          })
        } else {
          this.transportData.forEach(elem => {
            const cost_light = parseFloat(elem.cost_transport_light.replace(/[^\d.]/g, ''));
            if(cost_light < cheapest && elem.city === destination) {
              cheapest = cost_light;
              res = elem;
            }
          });
        }


        return {
          name: res.name,
          cost: weight * cheapest,
          lead_time: res.lead_time
        }

      } catch (err) {
        alert('Erro:' + err)
        return null;
      }
    },

    getFastest() {
      try {
        if(!this.dadosForm) return null;
        const destination = this.dadosForm.destination;
        const weight = this.dadosForm.weight
        let res = {};
        let price;
        let fastest = 'init';

        this.transportData.forEach(elem => {
          if (this.compareHours(elem.lead_time, fastest) && elem.city === destination) {
            fastest = elem.lead_time;
            price = (weight > 100? elem.cost_transport_heavy : elem.cost_transport_light)
            res = elem;
          }
        })

        return {
          name: res.name,
          cost: weight * parseFloat(price.replace(/[^\d.]/g, '')),
          lead_time: res.lead_time
        }

      } catch (err) {
        alert('Erro:' + err)
        return null;
      }
    },

    compareHours(h1, h2) {
      if(h2 === 'init') return h1;

      let [h1format, h2format] = [h1, h2]

      if (h1[h1.length] === 'h') {
        h1format = h1format.slice(0, -1);
        h1format + '00';
      } else {
        h1format = h1format.slice(0, -3) + h1format.slice(-2, h1format.length);
      }

      if (h2[h2.length] === 'h') {
        h2format = h2format.slice(0, -1);
        h2format + '00';
      } else {
        h2format = h2format.slice(0, -3) + h2format.slice(-2, h2format.length);
      }

      if(parseInt(h1format) < parseInt(h2format)) return h1;

      return h2;

    }

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

.bg-custom {
  background-color: #5f97b9;
}

.custom-txt {
  font-size: 24px;
  font-weight: bold;
}

.logo {
  width: 30px;
  height: auto;
  margin-right: 10px;
  margin-left: 20px;
}

.alignItems {
  display: flex;
  align-items: center;
}

.center-all {
  display: flex;
  justify-content: center;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.2);
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  position: relative;
}
.clear {
  position: absolute;
  bottom: 0;
  right: 0;
  margin-bottom: 10px;
  margin-right: 10px;
  background-color: #85b8c5;
  border: none;
}

</style>