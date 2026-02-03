<script setup>
  import { ref } from 'vue'
  import Button from './components/Button.vue'
  import Header from './components/Header.vue'
  import Card from './components/Card.vue'

  let isGameStart = ref(false)
  const startGame = () => {
    isGameStart.value = true
  }
</script>

<template>
  <div class="main">
    <Header></Header>
    <div v-if="!isGameStart" class="container">
      <Button @click="startGame">Начать игру</Button>
    </div>
    <div v-else class="container">
      <Card>
        <template #card-number>01</template>
        unadmitted
      </Card>
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
}
</style>
