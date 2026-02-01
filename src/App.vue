<script setup>
  import { ref } from 'vue'

  const date = new Date()
  const time = ref('')
  calcTime()
  function calcTime() {
    const currentDateTime = new Date()
    let currentTime = ''
    currentTime = currentDateTime.getHours()
    currentTime += ':'
    currentTime += currentDateTime.getMinutes()
    currentTime += ':'
    currentTime += currentDateTime.getSeconds() < 10 ? '0' + currentDateTime.getSeconds() : currentDateTime.getSeconds()
    time.value = currentTime
  }
  setInterval(() => {
    calcTime()
  }, 1000)
</script>

<template>
  <div>
    <p>Текущая дата: <strong>{{  date.toLocaleDateString() }}</strong></p>
    <p>Текущее время: <strong>{{ time }}</strong></p>
  </div>
</template>

<style scoped>
</style>
