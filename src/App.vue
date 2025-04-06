<script setup>
import Header from '@/components/Header.vue'
import CurrentIssue from './components/CurrentIssue.vue';
import SectionResponseAndDescription from './components/SectionResponseAndDescription.vue';
import MyBtn from './components/MyBtn.vue';
import { onMounted, provide, ref } from 'vue';

const URL_SONG_BIRD = "https://xeno-canto.org/api/2/recordings?query=cnt:brazil";
const infoBird = ref(null);

// Создаю рандоманое число что бы каждый раз была новая запись изначально
const randomNumber = ref(0);
const generateRandom = () => {
  randomNumber.value = Math.floor(Math.random() * 500); // От 0 до 499
};

// Принятие API звуков птиц и provide на другие компоненты их
onMounted(async () => {
  try {
    const response = await fetch(URL_SONG_BIRD);
    const data = await response.json();
    console.log(data);
    generateRandom()
    console.log(randomNumber.value)
    infoBird.value = data.recordings[randomNumber.value]; 
  } catch (error) {
    console.error("Нихуя не работает");
  }
});
provide('infoBird', infoBird); 
</script>

<template>
  <header class='m-5'>
    <Header></Header>
  </header>
  <main>
    <CurrentIssue></CurrentIssue>
    <SectionResponseAndDescription></SectionResponseAndDescription>
    <MyBtn></MyBtn>
  </main>
</template>

<style>
</style>