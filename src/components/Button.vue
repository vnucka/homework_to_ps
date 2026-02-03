<script setup>
  const { style } = defineProps({
    style: {
      type: String,
      default: 'filled',
      validator: (value) => {
        return ['transparent', 'icon', 'filled'].includes(value)
      }
    },
    uppercase: {
      type: Boolean,
      default: false
    },
    textSize: {
      type: String,
      default: 'normal',
      validator: (value) => {
        return ['small', 'normal', 'large'].includes(value)
      }
    },
    textWeight: {
      type: [String, Number],
      default: 400,
      validator(value) {
        return [400, 500, 600, 700].includes(+value)
      }
    }
  })
</script>
<template>
    <button
        :class="[
            'button',
            style,
            `text-${textSize}`,
            `weight-${textWeight}`,
            {
              uppercase
            }
        ]">
      <slot></slot>
    </button>
</template>
<style scoped>
    .button {
        text-align: center;
        border: none;
        transition: 0.5s;
        background: none;
      &.weight-400 {
        font-weight: 400;
      }
      &.weight-500 {
        font-weight: 400;
      }
      &.weight-600 {
        font-weight: 600;
      }
      &.weight-700 {
        font-weight: 700;
      }
      &.text-small {
        font-size: 12px;
        line-height: 18px;
      }
      &.text-normal {

      }
      &.text-large {
        font-size: 24px;
        line-height: 36px;
        letter-spacing: 0;
      }
      &.uppercase {
        text-transform: uppercase;
      }
      &.filled {
        width: 315px;
        border-radius: 100px;
        padding: 16px 10px;
        color: var(--color-text-primary-invert);
        background: var(--color-primary);
        &:hover {
          background: var(--color-primary-darken);
        }
      }
      &.transparent {
        color: var(--color-text-primary);
      }
    }
</style>