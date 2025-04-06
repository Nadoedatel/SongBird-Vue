<script setup>
import { inject } from 'vue';
let radnomImagesCat = inject('radnomImagesCat')
const infoBird = inject('infoBird'); 
console.log(infoBird.value); 
</script>

<template> 
    <div class='flex flex-col gap-5 items-center border-[#383838] border-2 bg-[#303030] m-5 p-5 text-white'>
        <div class='flex items-center gap-5'>
            <div>
                <img :src="radnomImagesCat" alt="Image-bird">
            </div>
            <div v-if="infoBird">
                <p>{{ infoBird.gen }}</p>
                <hr>
                <p>{{ infoBird.group }}</p>
                <hr>
                <audio controls :src="infoBird.file"></audio>
            </div>
            <div v-else>
                <p>Идет загрузка...</p>
            </div>
        </div>
        <div>
            Descriptions Bird
        </div>
    </div>
</template>

<style> 
</style>