<script setup>
import { inject, ref, watch } from 'vue';


const isCooldown = ref(false);
const isLoading = inject('isLoading')

watch(isLoading, () => {
  console.log(isLoading.value);
  handleNextLevel()
});

const handleNextLevel = () => {
  if (isLoading.value) {
    console.log("Кнопко не доступна");
    isCooldown.value = true;
  } else {
    console.log("Кнопко доступна");
    isCooldown.value = false;
  }
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