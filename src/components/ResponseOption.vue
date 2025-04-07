<script setup>
import { inject } from 'vue';


const infoBird = inject('infoBird');

</script>

<template> 
    <div class='flex items-center border-[#383838] border-2 bg-[#303030] m-5 p-5 text-white'>
        <div v-if="infoBird" class='flex items-center gap-5'>
            <input type="radio" id="one">
            <p>{{ infoBird.gen }}</p>
        </div>
        <div v-else>
            <p>Идет загрузка...</p>
        </div>
    </div>
</template>

<style> 
</style>