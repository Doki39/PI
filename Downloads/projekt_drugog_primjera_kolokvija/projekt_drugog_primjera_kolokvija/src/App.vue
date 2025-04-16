<script setup>
    import Zadatak_1 from './components/Zadatak_1.vue';
    import Zadatak_2 from './components/Zadatak_2.vue';
    import Zadatak_3 from './components/Zadatak_3.vue';
</script>

<template>
    <div>  
        <!--Zadaci se rješavaju unutar komponenti-->
        <!--Za biranje zadataka treba mjenjati true/false-->
        <Zadatak_1 v-if="false"/>
        <Zadatak_2 v-if="false"/>
        <Zadatak_3 v-if="true"/>
    </div>
</template>