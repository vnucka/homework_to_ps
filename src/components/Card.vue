<script setup>
import Button from './Button.vue'
import IconSuccess from '../icons/IconSuccess.vue'
import IconError from '../icons/IconError.vue'
import {ref} from 'vue'
defineProps({
  cardNumber: {
    type: String,
    default: '01'
  },
  cardStatus: {
    type: String,
    default: 'pending',
    validator: (value) => {
      return ['pending', 'fail', 'success'].includes(value)
    }
  },
  cardText: {
    type: String,
    default: ''
  },
  cardTextTranslate: {
    type: String,
    default: ''
  }
})

let status = ref('shirt')
const rotate = () => {
  if(status.value === 'shirt') {
    status.value = 'value'
  } else {
    status.value = 'shirt'
  }
}
</script>

<template>
  <div
      :class="[
          'card',
          {
            'card-shirt': status === 'shirt',
            'card-value': status === 'value'
          }
      ]">
    <div class="card-container">
      <div class="card-header">
        <div class="card-number"> {{ cardNumber }} </div>
        <div
            v-if="cardStatus !== 'in-game'"
            class="card-status">
          <IconSuccess v-if="cardStatus === 'success'" />
          <icon-error v-if="cardStatus === 'fail'" />
        </div>
      </div>
      <div v-if="status === 'shirt'" class="card-body">
        {{ cardText }}
      </div>
      <div v-else class="card-body">
        {{ cardTextTranslate }}
      </div>
      <div class="card-footer">
        <Button
            :style="'transparent'"
            :uppercase="true"
            text-weight="700"
            @click="rotate"
        >Перевернуть</Button>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .card {
    max-width: 210px;
    cursor: pointer;
    box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.1);
    transition: 0.3s;
    background: #FFFFFF;
    padding: 28px 20px;
    border-radius: 16px;
    transform-style: preserve-3d;
    &:hover {
      box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.1), 10px 10px 10px 0px rgba(0, 0, 0, 0.05);
    }
    &.card-value {
      transform: rotateY(180deg);
      .card-container {
        transform: rotateY(180deg);
      }
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
    display: flex;
    position: relative;
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
    letter-spacing: 0;
    .card-number {
      color: var(--color-text-secondary);
      transform: translate(16px, -7px);
    }
    .card-status {
      position: absolute;
      left: 50%;
      transform: translate(-50%, -50%);
    }
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