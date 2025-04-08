<script setup>
import { ref } from 'vue';


const isCooldown = ref(false);

const handleNextLevel = () => {
  if (isCooldown.value) return;
  
  isCooldown.value = true;
  
  // Автоматическая разблокировка через 2 секунды
  setTimeout(() => {
    isCooldown.value = false;
  }, 4000);
};

</script>

<template>
     <button 
    class="p-2 bg-[#3db390] m-5 text-white rounded-xl w-full hover:bg-[#318b70] disabled:opacity-50"
    @click="handleNextLevel"
    :disabled="isCooldown"
  >
    Next Level
  </button>
</template>

<style> 
</style>