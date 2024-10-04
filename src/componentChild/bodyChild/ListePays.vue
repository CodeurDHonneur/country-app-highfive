<script setup>
import { ref, computed, watch, onMounted } from "vue";
import IconRecherche from '@/components/icons/IconRecherche.vue';
const props = defineProps(['listes']);
const filtrage = ref(""); //valeur de filtrage des données

const lengthFiltrage = ref(0);


const restart = () => {
  filtrage.value = "";
};

const dataFilter = computed(() => {
  const dataSort = props.listes.sort((a, b) => a.nom - b.nom);

  if(filtrage.value == "") {
    return dataSort;
  } else {
    const data = dataSort.filter(item => item.nom.toLowerCase().includes(filtrage.value.toLowerCase()));
    lengthFiltrage.value = data.length;
    return data;
  }
});




</script>

<template>
    <article>
        <div class="entete">
          <h2>Liste des pays </h2>
          <p>Total pays : {{ listes.length  }}</p>
          <p>Total recherche : {{ lengthFiltrage }}</p>
          <div  class="form">
            <input type="text" v-model.trim="filtrage">
            <button @click="restart">
                <IconRecherche />
            </button>
          </div>
        </div>
        <div class="liste">
          <ul >
            <li v-for="(liste, index) in dataFilter" :key="liste.id">
                <span>{{ index + 1 }}.  </span>
                <span>{{ liste.nom }}</span>
                <div class="parent-image">
                    <img :src="liste.drapeau" :alt="liste.nom" :title="liste.nom" class="drapeau">
                </div>
            </li>
        </ul>
        </div>
       
      
    </article>
</template>

<style scoped>
article{
    background-color: white;
    border-radius: 3%;
    padding: 20px;
    width: 300px;
    height: 500px;
    
  }

  .liste {
    overflow-y: scroll;
    max-height: 300px;
    
  }
  .parent-image {
    display: inline-block;
    width: 15px;
    margin-left: 12px;
  }
  ul {
    list-style: none;
    padding-left: 0;
  }
  .drapeau {
    width: 100%;
  }

  .form {
    border: 2px solid black;
    border-radius: 6px;
    display: flex;
  }

  input {
    border: none;
    width: 90%;
  }
  .entete {
    text-align: center;
  }
</style>