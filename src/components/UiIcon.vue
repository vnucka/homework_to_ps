<script setup>
  import { defineAsyncComponent, computed } from 'vue'
  const { size, name } = defineProps({
    size: {
      type: [Number, String],
      default: 48,
      validator: value => [12, 24, 48].includes(+value),
    },
    name: {
      type: String,
      default: null
    }
  })
  const icons = import.meta.glob('../icons/*.vue')
  const Icon = computed(() => {
    const path = `../icons/${name}.vue`
    return icons[path]
        ? defineAsyncComponent(icons[path])
        : null
  })

</script>

<template>
  <component :is="Icon" :class="'size-' + size" />
</template>

<style scoped>

.size-12 {
  width: 12px;
  height: 12px;
}
.size-24 {
  width: 24px;
  height: 24px;
}
.size-48 {
  width: 48px;
  height: 48px;
}
</style>