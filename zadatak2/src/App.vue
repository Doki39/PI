<template>

<div class=" flex flex-col gap-4">
    <div class="text-left">
        <div class="w-120 h-38 bg-blue-200 border-2 rounded-2xl px-3 pt-1">
        <h1 class="text-2xl py-2 text-blue-950">Korisnicki podaci</h1>
        <div class="w-110 h-0.5 rounded-3xl bg-blue-300"></div>
        <h1 class="pt-2 text-blue-950">Ime: 
            <span :class="calculatedClass()">{{ korisnik.osobni_podaci.ime }} {{ korisnik.osobni_podaci.prezime }}</span></h1>
        <h1 class="text-blue-950">Adresa: 
            <span :class="calculatedClass()">{{ korisnik.osobni_podaci.adresa.grad }}, {{ korisnik.osobni_podaci.adresa.ulica }} {{ korisnik.osobni_podaci.adresa.broj }} </span></h1>
        <h1 class="text-blue-950">Telefon: 
            <span :class="calculatedClass()">{{ korisnik.osobni_podaci.broj_telefona }} </span></h1>
        </div>
    </div>
        <div class="w-120 h-160 bg-blue-200 border-2 rounded-2xl px-4.5 flex flex-col gap-3">
            <h1 class="text-2xl text-black pt-3 pl-2">Kosarica</h1>
            <div class="w-110 h-30 bg-blue-100 rounded-2xl -border border-2 border-gray-400 flex items-center gap-3 pl-2">
                <img :src="slika.Jabuka" alt="Jabuka " class="size-18"> 
                    <div class="details flex flex-col">
                    <h1 class="text-black text-2">{{ proizvodi[0].naziv }}</h1>
                    <h1 class="text-black">Cijena: €{{ proizvodi[0].cijena }} | Kolicina: {{ korisnik.kosarica[0].kolicina }}</h1>
                    <h1 class="text-black">Ukupno: €{{ calcPrice(proizvodi[0].cijena, korisnik.kosarica[0].kolicina).toFixed(2) }} </h1>
                    </div>
                </div>
                <div class="w-110 h-30 bg-blue-100 rounded-2xl -border border-2 border-gray-400 flex items-center gap-3 pl-2">
                <img :src="slika.Mrkva" alt="Mrkva " class="size-18"> 
                    <div class="details flex flex-col">
                    <h1 class="text-black text-2">{{ proizvodi[1].naziv }}</h1>
                    <h1 class="text-black">Cijena: €{{ proizvodi[1].cijena }} | Kolicina: {{ korisnik.kosarica[1].kolicina }}</h1>
                    <h1 class="text-black">Ukupno: €{{ calcPrice(proizvodi[1].cijena, korisnik.kosarica[1].kolicina).toFixed(2) }} </h1>
                    </div>
                </div>
                <div class="w-110 h-30 bg-blue-100 rounded-2xl -border border-2 border-gray-400 flex items-center gap-3 pl-2">
                <img :src="slika.Kruh" alt="Kruh" class="size-18"> 
                    <div class="details flex flex-col">
                    <h1 class="text-black text-2">{{ proizvodi[2].naziv }}</h1>
                    <h1 class="text-black">Cijena: €{{ proizvodi[2].cijena }} | Kolicina: {{ korisnik.kosarica[2].kolicina }}</h1>
                    <h1 class="text-black">Ukupno: €{{ calcPrice(proizvodi[2].cijena, korisnik.kosarica[2].kolicina).toFixed(2) }} </h1>
                    </div>
                </div>
                <div class="w-110 h-30 bg-blue-100 rounded-2xl -border border-2 border-gray-400 flex items-center gap-3 pl-2">
                <img :src="slika.Sir" alt="Sir" class="size-18"> 
                    <div class="details flex flex-col">
                    <h1 class="text-black text-2">{{ proizvodi[3].naziv }}</h1>
                    <h1 class="text-black">Cijena: €{{ proizvodi[3].cijena }} | Kolicina: {{ korisnik.kosarica[3].kolicina }}</h1>
                    <h1 class="text-black">Ukupno: €{{ calcPrice(proizvodi[3].cijena, korisnik.kosarica[3].kolicina).toFixed(2) }} </h1>
                    </div>
                </div>
            <h1 class="text-black"> Ukupna cijena:  {{ totalPrice.toFixed(2) }} <span></span></h1>
        </div>

</div>

</template>


<script setup>
    import { ref, computed } from 'vue'
    import data from './data.json'

    const isAdmin = ref(true);

    const korisnik = data.korisnik
    const slika = data.slike
    const proizvodi = data.proizvodi

    function calcPrice(cijena, kolicina) {
        return cijena * kolicina;
    }

   
    const totalPrice = computed(() => {
        return korisnik.kosarica.reduce((total, item, index) => {
            const product = proizvodi[index]; 
            return total + calcPrice(product.cijena, item.kolicina); 
        }, 0);
    });

    const calculatedClass = () => ({
    'text-blue-500': isAdmin.value
    })


</script>
