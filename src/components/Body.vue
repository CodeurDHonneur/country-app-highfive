<script setup>

import ListePays from '@/componentChild/bodyChild/ListePays.vue'
import PremiereInfo from '@/componentChild/bodyChild/PremiereInfo.vue'
import SecondeInfo from '@/componentChild/bodyChild/SecondeInfo.vue'
import Drapeau from '@/componentChild/enteteChild/Drapeau.vue'
import StatistiquesGenerales from '@/componentChild/bodyChild/StatistiquesGenerales.vue'

const props = defineProps(['listePays'])


</script>

<template>
    <main>
        <div class="pays ">
            <Drapeau />
            <ListePays 
            :listes="listePays"/>
        </div>
        <div class="content">
            <div class="cap">
                <StatistiquesGenerales />
                <PremiereInfo />
            </div>
            <SecondeInfo />
        </div>
    </main>
</template>

<style scoped>
main{
    position: relative;
    background-color: whitesmoke;
    height: 700px;
  }
  
  .pays{
    float: left;
    width: 20%;
    margin-right: 100px;
    padding:  130px 0 0 30px;

  }
  

  .cap{
    display: flex;
  }
  

  .content{
    height: 600px;
    margin-left: 500px;
    padding: 30px;
  }

  

</style>