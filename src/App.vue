<script setup>
import {reactive, ref} from 'vue'
  import Button from './components/Button.vue'
  import Header from './components/Header.vue'
  import Card from './components/Card.vue'
  import gameItemsData from './gameItems.js'

  const isGameStart = ref(false)
  const gameScore = ref(0)
  const startGame = () => {
    isGameStart.value = true
  }

  function getRandomInt(min, max) {
    min = Math.ceil(min) // округляем до ближайшего большего целого
    max = Math.floor(max) // округляем до ближайшего меньшего целого
    return Math.floor(Math.random() * (max - min + 1)) + min // генерируем случайное целое число
  }

  const items = []
  while (items.length < 12) {
    const res = getRandomInt(0, 49)
    if (!items.includes(res)) {
      items.push(res)
    }
  }

  const gameItems = reactive([])
  items.forEach((item, key) => {
    gameItems.push({
      number: (key + 1) < 10 ? '0' + (key + 1) : (key + 1).toString(),
      text: gameItemsData[item].text,
      translate: gameItemsData[item].translate,
      status: 'pending',
      state: 'closed'
    })
  })

  const selectCard = (card) => {
    if (event.target.classList.contains('button')) {
      return false
    }
    card.status = 'win'
    gameScore.value++
  }
  const toggleCardState = (card) => {
    card.state = (card.state === 'closed') ? 'opened' : 'closed'
  }
</script>

<template>
  <div class="main">
    <Header :game-score="gameScore"></Header>
    <div v-if="!isGameStart" class="container">
      <Button
          text-size="large"
          @click="startGame">Начать игру</Button>
    </div>
    <div v-else class="container game">
      <Card
          v-for="item in gameItems"
          :key="item.number"
          :card-number="item.number"
          :card-text="item.text"
          :card-text-translate="item.translate"
          :card-status="item.status"
          :state="item.state"
          @click="selectCard(item)"
          @toggle-card-state="toggleCardState(item)"
      />
    </div>
  </div>
</template>

<style scoped>
.main {
  height: 100%;
}
.container {
  display: grid;
  place-content: center;
  height: 100%;
  &.game {
    gap: 50px;
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>
