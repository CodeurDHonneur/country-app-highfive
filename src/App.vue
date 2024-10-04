<script setup>
import Body from '@/components/Body.vue';
import Entete from '@/components/Entete.vue';
import { onMounted, reactive, ref } from 'vue';

const countryData = ref([]);
const listeNomPays = ref([]);

let id = ref(0);

let obj = ref({
    id: "",
    drapeau: "",
    langues: "",
    nom: "",
    continent: "",
    region: "",
    capital: "",
    demarrageSemaine: "",
    status: "",
    population: "",
    superficie: ""
})

let objListePays = reactive({
  id: "",
  nom: "",
  drapeau: ""
});

function reinitialiseObj(){
  obj.value = {
    id: "",
    drapeau: "",
    langues: "",
    nom: "",
    continent: "",
    region: "",
    capital: "",
    demarrageSemaine: "",
    status: "",
    population: "",
    superficie: ""
  }
};

function reinitialiseObjListePays(){
  objListePays = { id: "",nom: "",drapeau: ""}
};

function formatData(array, length) {
  for(let i = 0; i < length; i++){
      obj.value.id = i,
      obj.value.drapeau = array[i].flags.png,
      obj.value.langues = array[i].languages,
      obj.value.nom = array[i].name.common,
      obj.value.continent = array[i].continents,
      obj.value.region = array[i].region,
      obj.value.capital = array[i].capital,
      obj.value.demarrageSemaine = array[i].startOfWeek,
      obj.value.status = array[i].independent,
      obj.value.population = array[i].population,
      obj.value.superficie = array[i].area,

      countryData.value.push(obj.value);
      reinitialiseObj();
  }
};

function addListePays(array, length){
  for(let i = 0; i < length; i++){ 
    objListePays.id = i,
    objListePays.nom = array[i].name.common,
    objListePays.drapeau = array[i].flags.png,

    listeNomPays.value.push(objListePays);
    reinitialiseObjListePays();
  }
};


const dataCountry = () => {
  return fetch('https://restcountries.com/v3.1/all')
    .then((res) => res.json())
    .then(response => {
      const length = response.length;
      formatData(response,length);
      addListePays(response, length);
    }
    )
    .catch(error => console.log('Error', error));
};

console.log(countryData.value);
onMounted(() => {
  dataCountry();
});
</script>

<template>
  <div class="container">
    <Entete></Entete>

    <Body 
    :listePays="listeNomPays"
    ></Body>
   
  </div>

</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.container {
  height: 100%;
  padding: 5px 10%;
}
</style>
