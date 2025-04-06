<script setup>
import { inject } from 'vue';

const infoBird = inject('infoBird'); 
let radnomImagesCat = inject('radnomImagesCat')
console.log(infoBird.value); 
</script>

<template>
    <div class='flex items-center gap-10 bg-[#303030] m-5 p-5 text-white'>
        <div>
            <img :src="radnomImagesCat" alt="Image-bird">
        </div>
        <div v-if="infoBird">
            <p>{{ infoBird.gen }}</p>
            <hr>
            <audio controls :src="infoBird.file"></audio>
        </div>
        <div v-else>
            <p>Идет загрузка...</p>
        </div>
    </div>    
</template>

<style> 
</style>