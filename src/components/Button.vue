<script setup></script>
<template>
    <button class="button"><slot></slot></button>
</template>
<style scoped>
    .button {
        width: 315px;
        border-radius: 100px;
        padding: 16px 10;
        font-size: 24px;
        line-height: 36px;
        letter-spacing: 0%;
        text-align: center;
        border: none;
        background: var(--color-primary);
        color: var(--color-text-primary-invert);
        transition: 0.5s;
    }
    .button:hover {
        background: var(--color-primary-darken);
    }
</style>