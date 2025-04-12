<script setup>
 import { ref } from "vue";
 import { computed } from "vue";

 const Kolicina = ref(1)
 const newProductName = ref('')
 const newProductPrice = ref('')
 const Product = ref([
 { "naziv": "Jabuka", "Kolicina": 4, "cijena": 0.25 },
 { "naziv": "Banana", "Kolicina": 12, "cijena": 0.12 },
 { "naziv": "Lubenica", "Kolicina": 1, "cijena": 4.48 },
 { "naziv": "Kruh", "Kolicina": 3, "cijena": 2 }
 ]);

 function removeProduct(index) {
  Product.value.splice(index, 1);
 }

 const totalPrice = computed(() => {
  return Product.value.reduce((sum, item) => {
    return sum + item.cijena * item.Kolicina;
  }, 0);

});


function povecaj(index) {
  Product.value[index].Kolicina++;
}

function smanji(index) {
  if (Product.value[index].Kolicina > 0) {
    Product.value[index].Kolicina--;
  }
}

function addProduct() {
  Product.value.push({
    naziv: newProductName.value, 
    cijena: parseFloat(newProductPrice.value),
    Kolicina
  });
  newProductName.value = ""
  newProductPrice.value = ""

}


</script>
<template>

<div class="box-border-2 size-220 h-180 rounded-2xl bg-white pl-7 flex flex-col">

    <h1 class="text-3xl py-5">Kosarica</h1>
    <div class=" w-200 mx-10 h-0.5 rounded-2xl bg-gray-500"></div>
    <div class="flex flex-row gap-3 py-5">
    <h1>
    Naziv proizvoda:
    <input type="text" v-model="newProductName" class="border px-1 w-50 rounded h-8"
    placeholder="Upisi naziv proizvoda...">
    </h1>
    <h1>
    Cijena proizvoda:
    <input type="text" v-model="newProductPrice" class="border px-1 w-50 rounded h-8"
    placeholder="Upisi cijenu proizvoda...">
    </h1>
    <div  v-if="newProductName !==0 && newProductPrice > 0">
    <button @click="addProduct()" class="w-30 h-8 bg-green-700 hover:cursor-pointer">Dodaj artikl</button>
    </div>
    <div  v-else>
      <button @click="" class="w-30 h-8 bg-red-700 hover:cursor-pointer">Dodaj artikl</button>
    </div>
    

    </div>


      <div class=" w-200 mx-10 h-0.5 rounded-2xl bg-gray-500"></div>

      <div class="flex flex-row gap-30 py-5">
      <h1 class="text-2xl">Naziv</h1>
      <h1 class="text-2xl">Kolicina</h1>
      <h1 class="text-2xl">Cijena</h1>
      <h1 class="text-2xl">Ukupno</h1>
      </div>
      
      <div v-for="(item, index) in Product" class="bg-gray-400 w-200 border-1 border-black h-12 rounded flex items-center  px-4">

        <span class="w-40">{{ item.naziv }}</span>

        <div class="flex items-center w-50">
        <button @click="smanji(index)" class="bg-red-500 text-white px-2 py-0.5 rounded">-</button>
        <input  
         v-model="item.Kolicina" 
        min="0" 
        class="border rounded w-20"/>
       
        <button @click="povecaj(index)" class="bg-red-500 text-white px-2 py-0.5 rounded">+</button>
        </div>
        <span class="w-50">€{{ item.cijena }}</span>
        <span class="w-25">€{{ (item.cijena * item.Kolicina).toFixed(2) }}</span>

        <button @click="removeProduct(index)" class="hover:cursor-pointer text-red-800 "> Ukloni</button>
      </div>
      <div class="pt-25 pb-5">
      <div class=" w-200 mx-10 h-0.5 rounded-2xl bg-gray-500"></div>
      </div>
      <div>
        <b>Ukupno:</b> <Span> €{{ totalPrice.toFixed(2) }}</Span>
      </div>
</div>
</template>
