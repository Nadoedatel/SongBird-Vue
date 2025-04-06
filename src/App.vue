<script setup>
import Header from '@/components/Header.vue'
import CurrentIssue from './components/CurrentIssue.vue';
import SectionResponseAndDescription from './components/SectionResponseAndDescription.vue';
import MyBtn from './components/MyBtn.vue';
import { onMounted, provide, ref } from 'vue';

const URL_SONG_BIRD = "https://xeno-canto.org/api/2/recordings?query=cnt:brazil";
const infoBird = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(URL_SONG_BIRD);
    const data = await response.json();
    console.log(data);
    infoBird.value = data.recordings[0]; 
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