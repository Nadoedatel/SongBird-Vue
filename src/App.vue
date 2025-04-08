<script setup>
import Header from '@/components/Header.vue'
import CurrentIssue from './components/CurrentIssue.vue';
import SectionResponseAndDescription from './components/SectionResponseAndDescription.vue';
import MyBtn from './components/MyBtn.vue';

import { onMounted, provide, ref } from 'vue';

const URL_SONG_BIRD = "https://xeno-canto.org/api/2/recordings?query=cnt:belarus";

// Реактивные данные
const infoBird = ref(null);
const birdArr = ref([]);
const randomImagesCat = ref("https://cataas.com/cat");
const isLoading = ref(false);
const error = ref(null);
const scoreCount = ref(0)

// // Количество вопросов и все переменные для этой фунециии
// const currentQuestionIndex = ref(0);
// const countQuestion = 10
// const quizQuestions = ref([]);

// // Создание заранее 10 вопросов

// async function createArrQuestion() {
//   try {
//     isLoading.value = true;
//     error.value = null;
    
//     const response = await fetch(URL_SONG_BIRD);
//     if (!response.ok) throw new Error("Ошибка API");
//     const data = await response.json();
//     const usedIndices = new Set();
    
//     // Очищаем массив перед заполнением
//     quizQuestions.value = [];

//     for (let i = 0; i < countQuestion; i++) {
//       // Выбираем правильный ответ
//       const correctIndex = getUniqueRandomIndex(data.recordings.length, usedIndices);
//       usedIndices.add(correctIndex);
//       const correctBird = data.recordings[correctIndex];
      
//       // Выбираем 5 случайных вариантов
//       const optionIndices = [];
//       while (optionIndices.length < 5 && usedIndices.size < data.recordings.length) {
//         const index = getUniqueRandomIndex(data.recordings.length, usedIndices);
//         optionIndices.push(index);
//         usedIndices.add(index);
//       }
      
//       // Формируем вопрос
//       const allIndices = shuffleArray([correctIndex, ...optionIndices]);
//       const question = {
//         correctBird,
//         options: allIndices.map(index => ({
//           ...data.recordings[index],
//           isCorrect: index === correctIndex
//         }))
//       };
      
//       quizQuestions.value.push(question);
//     }
    
//     // Загружаем первый вопрос
//     loadQuestion(0);
    
//   } catch (err) {
//     error.value = err.message;
//     console.error("Ошибка при создании вопросов:", err);
//   } finally {
//     isLoading.value = false;
//   }
// }

// // Переход к следующему вопросу
// function nextQuestion() {
//   loadQuestion(currentQuestionIndex.value + 1);
// }
// provide('nextQuestion',nextQuestion)
// // Загрузка конкретного вопроса
// function loadQuestion(index) {
//   if (index >= quizQuestions.value.length) return;
  
//   currentQuestionIndex.value = index;
//   const question = quizQuestions.value[index];
  
//   infoBird.value = question.correctBird;
//   birdArr.value = question.options;
// }
// Объявляем provide в setup() ДО onMounted
provide('infoBird', infoBird);
provide('birdArr', birdArr);
provide('randomImagesCat', randomImagesCat);

// Функции для работы с данными
function getUniqueRandomIndex(max, usedIndices) {
  let index;
  do {
    index = Math.floor(Math.random() * max);
  } while (usedIndices.has(index));
  return index;
}

function shuffleArray(array) {
  return [...array].sort(() => Math.random() - 0.5);
}

async function loadBirdData() {
  try {
    isLoading.value = true;
    error.value = null;
    
    const response = await fetch(URL_SONG_BIRD);
    if (!response.ok) throw new Error("Ошибка API");
    
    const data = await response.json();
    const usedIndices = new Set();
    
    // Из LocalStorage получаем значение пользователя
    scoreCount.value = localStorage.getItem('Score')

    // Выбираем правильный ответ
    const correctIndex = getUniqueRandomIndex(data.recordings.length, usedIndices);
    usedIndices.add(correctIndex);
    infoBird.value = data.recordings[correctIndex];
    
    // Выбираем 5 случайных записей
    const randomIndices = [];
    while (randomIndices.length < 5 && usedIndices.size < data.recordings.length) {
      const index = getUniqueRandomIndex(data.recordings.length, usedIndices);
      randomIndices.push(index);
      usedIndices.add(index);
    }
    
    // Формируем итоговый массив
    const allIndices = shuffleArray([correctIndex, ...randomIndices]);
    birdArr.value = allIndices.map(index => ({
      ...data.recordings[index],
      isCorrect: index === correctIndex
    }));
  } catch (err) {
    error.value = err.message;
    console.error("Ошибка при загрузке данных:", err);
  } finally {
    isLoading.value = false;
  }
}

// Счетчик правильных ответов
const incrementScore = () => {
  scoreCount.value++;
  localStorage.setItem("Score", scoreCount.value)
  console.log('Текущий счет:', scoreCount.value);
};
provide('incrementScore', incrementScore)
provide('scoreCount', scoreCount);

// Загрузка данных при монтировании
onMounted(loadBirdData);
</script>

<template>
  <header class='m-5'>
    <Header></Header>
  </header>
  <main>
    <CurrentIssue></CurrentIssue>
    <SectionResponseAndDescription></SectionResponseAndDescription>
    <MyBtn @click="loadBirdData"></MyBtn>
  </main>
</template>

<style>
</style>