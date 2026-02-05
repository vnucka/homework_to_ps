<script setup>
import Score from './Score.vue'
const { gameScore } = defineProps({
  gameScore: {
    type: Number,
    default: 0
  }
})
</script>

<template>
    <header class="page-header">
        <h1>Запомни слово</h1>
        <Score :score="gameScore" />
    </header>
</template>

<style scoped>
    .page-header {
        display: flex;
        justify-content: space-between;
    }

    h1 {
        font-weight: 700;
        font-size: 16px;
        line-height: 24px;
        letter-spacing: 12%;
        text-transform: uppercase;
    }
</style>

