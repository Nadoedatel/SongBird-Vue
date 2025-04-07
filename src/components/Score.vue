<script setup>
import { inject} from 'vue';

const scoreCount = inject('scoreCount', 0);
</script>

<template>
    <div>
        <p class='text-white'>Score: {{ scoreCount }}</p>
    </div>
</template>

<style>

</style>