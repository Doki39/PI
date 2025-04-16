<script setup>

    import { ref } from 'vue'


    const broj1 = ref (1)
    const broj2 = ref (1)
    const operacija = ref ('')


    function provjeraOperacije () {
        if( operacija.value == "zbrajanje" || operacija.value == "oduzimanje" || operacija.value == "mnozenje" || operacija.value == "dijeljenje") {
        return true;
        }
        return false;
    }



</script>

<template>
<div class="flex flex-row gap-1">
<input type="number" v-model="broj1" class=" border-2 border-black">
<input type="number" v-model="broj2" class=" border-2 border-black">
<input type="text" v-model="operacija" class=" border-2 border-black">
</div> 


<div v-if = "!provjeraOperacije()">  Kriva operacija </div>
<div v-else-if="operacija == 'zbrajanje'">{{ broj1 + broj2 }}</div>
<div v-else-if="operacija == 'oduzimanje'">{{ broj1 - broj2 }}</div>
<div v-else-if="operacija == 'mnozenje'">{{ broj1 * broj2 }}</div>
<div v-else-if="operacija == 'dijeljenje' && broj2 > 0"> {{ broj1 / broj2 }} </div>
<div v-else-if="broj2 == 0"> Dijeljenje s nulom nije moguce</div>



</template>

<style scoped>

</style>