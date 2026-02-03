<script setup>

import Button from './Button.vue'
</script>

<template>
  <div class="card">
    <div class="card-container">
      <div class="card-header">
        <slot name="card-number"></slot>
      </div>
      <div class="card-body">
        <slot />
      </div>
      <div class="card-footer">
        <Button
            :style="'transparent'"
            :uppercase="true"
            text-weight="700"
        >Перевернуть</Button>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .card {
    box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.1);
    transition: 0.3s;
    background: #FFFFFF;
    padding: 28px 20px;
    border-radius: 16px;
    &:hover {
      box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.1), 10px 10px 10px 0px rgba(0, 0, 0, 0.05);
    }
  }
  .card-container {
    border-radius: 12px;
    border: 1px solid var(--color-secondary);
    height: 320px;
    width: 212px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .card-header {
    display: inline-block;
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    letter-spacing: 0;
    transform: translate(16px, -7px);
    color: var(--color-text-secondary);
  }
  .card-body {
    text-align: center;
    font-weight: 400;
    font-size: 18px;
    line-height: 100%;
    letter-spacing: 0;
    color: var(--color-text-secondary);
  }
  .card-footer {
    display: flex;
    justify-content: center;
    transform: translateY(9px);
  }
</style>