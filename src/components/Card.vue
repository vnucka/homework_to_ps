<script setup>
import Button from './Button.vue'
import UiIcon from './UiIcon.vue'
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
  },
  state: {
    type: String,
    default: 'closed'
  }
})

const emit = defineEmits(['toggleCardState', 'answer'])

const toggleCardState = () => {
  emit('toggleCardState')
}

const setAnswer = (answer) => {
  emit('answer', answer)
}
</script>

<template>
  <div
      :class="[
          'card',
          {
            'card-closed': state === 'closed',
            'card-opened': state === 'opened'
          }
      ]">
    <div class="card-container">
      <div class="card-header">
        <div class="card-number"> {{ cardNumber }} </div>
        <div
            v-if="cardStatus !== 'pending'"
            class="card-status">
          <UiIcon
              v-if="cardStatus === 'fail'"
              size="48"
              name="IconError"
          ></UiIcon>
          <UiIcon
              v-if="cardStatus === 'success'"
              size="48"
              name="IconSuccess"
          ></UiIcon>
        </div>
      </div>
      <div v-if="state === 'closed'" class="card-body">
        {{ cardText }}
      </div>
      <div v-else class="card-body">
        {{ cardTextTranslate }}
      </div>
      <div v-if="cardStatus === 'pending'" class="card-footer">
        <Button
            v-if="state === 'closed'"
            :style="'transparent'"
            :uppercase="true"
            text-weight="700"
            @click="toggleCardState"
        >Перевернуть</Button>
        <div v-else class="icon-btns">
          <Button :style="'icon'" @click="setAnswer(false)">
            <UiIcon
                size="24"
                name="IconError"
            ></UiIcon>
          </Button>
          <Button :style="'icon'" @click="setAnswer(true)">
            <UiIcon
                size="24"
                name="IconSuccess"
            ></UiIcon>
          </Button>
        </div>
      </div>
      <div v-else></div>
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
    &.card-opened {
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
    .button,
    .icon-btns {
      background: #FFFFFF;
    }
    .icon-btns {
      width: 100px;
      display: flex;
      justify-content: space-around;
      transform: translateY(7px);
    }
  }
</style>