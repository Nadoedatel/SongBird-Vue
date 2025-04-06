<script setup>
import { inject } from 'vue';

const infoBird = inject('infoBird'); // получим ref

// Для доступа к значению используем .value (если передали ref)
console.log(infoBird.value); 
</script>

<template>
    <div class='flex items-center gap-10 bg-[#303030] m-5 p-5 text-white'>
        <div>
            <img src="" alt="Image-bird">
        </div>
        <div>
            <p>{{ infoBird.gen }}</p>
            <hr>
            <div v-if="infoBird">
                    <audio controls :src="infoBird.file"></audio>
            </div>
            <div v-else>
                <p>Аудио не загружено или произошла ошибка.</p>
            </div>
        </div>
    </div>    
</template>

<style> 
</style>