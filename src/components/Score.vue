<script setup>
    import IconHeart from '../icons/IconHeart.vue'
    const { score } = defineProps({
      score: {
        type: Number,
        default: 0
      }
    })
</script>

<template>
    <div class="score">
        <div class="value">{{ score }}</div>
        <IconHeart />
    </div>
</template>

<style scoped>
    .score {
        display: flex;
        justify-content: center;
        background: var(--color-secondary);
        border-radius: 36px;
        padding: 12px 24px;
        gap: 10px;
    }
    .value {
        font-weight: 700;
        font-size: 16px;
        line-height: 24px;
        letter-spacing: 0%;
        color: var(--color-primary);
    }
</style>