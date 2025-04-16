<script setup>
    import { ref } from 'vue';

    const novoNatjecanje = ref('')


    const sportasi = ref([
        {
            ime: 'Ivan', 
            disciplina: 'plivanje', 
            godine: 25, 
            natjecanja: ['Olimpijske igre', 'Svjetsko prvenstvo']
        },
        {
            ime: 'Ana', 
            disciplina: 'atletika', 
            godine: 30, 
            natjecanja: ['Svjetsko prvenstvo', 'Europsko prvenstvo', 'Olimpijske igre']
        },
        {
            ime: 'Marko', 
            disciplina: 'odbojka', 
            godine: 22, 
            natjecanja: ['Europsko prvenstvo']
        }
    ])

    function  dodaj_natjecanje(sportasIndex){
        sportasi.value[sportasIndex].natjecanja.push({
            natjecanja: novoNatjecanje.value[sportasIndex]
        });

        novoNatjecanje.value=""

    }

    function ukloni_natjecanje(sportasIndex, natjecanjeIndex) {
          sportasi.value[sportasIndex].natjecanja.splice(natjecanjeIndex, 1);
       }


</script>

<template>

<div class="flex flex-col px-10 h-170 w-80 border-2 border-black">
  <h1 class="border-2 border-black w-60 mt-5">Svjetsko prvenstvo</h1>
  <div v-for="(sportas, sportasIndex) in sportasi" :key="sportasIndex">
    <h1>Ime: {{ sportas.ime }}</h1>
    <h1>Godine: {{ sportas.godine }}</h1>
    <h1>Disciplina: {{ sportas.disciplina }}</h1>
     <TransitionGroup name="list" tag="div">
    <h1>Natjecanja: <button @click="dodaj_natjecanje(sportasIndex)" class="border-1 px-1 hover:cursor-pointer ">+</button></h1>
   
    <div v-for="(natjecanje, natjecanjeIndex) in sportas.natjecanja" :key="natjecanjeIndex">
      <button @click="ukloni_natjecanje(sportasIndex, natjecanjeIndex)" class="border-1 px-1 hover:cursor-pointer">-</button>
      <input type="text"
        v-model="sportas.natjecanja[natjecanjeIndex]"
        placeholder="Upisi naziv natjecanja">
    </div>
    </TransitionGroup>
    <div class="h-0.5 w-55 bg-black my-3"></div>

  </div>
</div>



</template>

<style scoped>

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

</style>