
<script setup>

import { ref } from 'vue';

  const povecanaSlika = ref('')
  const galerija = [
    {
      slikar: "Pablo Picasso",
      godina: 1903,
      naslov: "The Old Guitarist",
      slika: "/src/assets/slike/The Old Guitarist.png"
    },
    {
      slikar: "Vincent van Gogh",
      godina: 1886,
      naslov: "Le Moulin de Blute-Fin",
      slika: "/src/assets/slike/Le Moulin de Blute-Fin.png"
    },
    {
      slikar: "Hokusai",
      godina: 1890,
      naslov: "Courtesan Asleep",
      slika: "/src/assets/slike/Courtesan Asleep.png"
    }
  ];

    function pictueAge(godina){
    return 2025-godina
     }

    function povecana_Slika(slikaIndex){
      povecanaSlika.value = galerija[slikaIndex].slika;
    }

</script>

<template>
  <div class="flex flex-col">
  <div class="flex flex-row gap-3">
  <div class="flex border-2 border-black m-5 items-left px-3 gap-5">
    <div v-for="(slika,slikaIndex) in galerija " :key="slikaIndex">
            <button @click="povecana_Slika(slikaIndex)" class="hover:cursor-pointer"><img :src="(slika.slika)" alt="" class="h-30"></button>
            <h1>Naslov: 
            <span :class="pictueAge(slika.godina) > 136? 'underline' : ''">
            {{ slika.naslov }} </span>
            </h1>
            <h1>Autor: {{ slika.slikar }}</h1>
            <h1>Starost: {{ pictueAge(slika.godina) }}</h1>
            </div>   
  
  </div>
  </div>    
  <img :src="povecanaSlika" alt="slika" class="size-130 mx-5"> 
 
</div>
</template>