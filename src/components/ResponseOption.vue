<script setup>
import { inject, ref } from 'vue';

const birdArr = inject('birdArr');
const infoBird = inject('infoBird'); 
const incrementScore = inject('incrementScore')

const selectedBirdId = ref(null)

const isTrueOrNot = (birdName) => {
    selectedBirdId.value = birdName.id;
    const isCorrect = birdName.gen === infoBird.value.gen;
    if (isCorrect) {
        incrementScore()
    }
    console.log(isCorrect ? "Верно!" : "Неверно!");
}

</script>

<template> 
    <div class='flex items-center border-[#383838] border-2 bg-[#303030] m-5 p-5 text-white'>
        <div v-if="birdArr">
            <div v-for="bird in birdArr" :key="bird.id"  @click="isTrueOrNot(bird)" class="flex items-center gap-5">
                <div class="flex items-center space-x-3 cursor-pointer">
                    <input class="absolute opacity-0 w-0 h-0" type="radio">
                    <div :id="bird.id" class="w-3 h-3 rounded-full flex items-center justify-center"
                    :class="{
                        'bg-[#444444]': selectedBirdId !== bird.id,
                        'bg-[#00bf8a]': selectedBirdId === bird.id && bird.gen === infoBird.gen,
                        'bg-[#d73010]': selectedBirdId === bird.id && bird.gen !== infoBird.gen
                        }"
                    </div>
                    <p>{{ bird.gen }}</p>
                </div>
            </div>
        </div>
        <div v-else>
            <p>Идет загрузка...</p>
        </div>
    </div>
</template>

<style scoped> 
</style>