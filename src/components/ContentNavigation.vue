<script setup>
import { watch } from 'vue'
import { useSlidesStore } from '@/stores/slides'
import { storeToRefs } from 'pinia'

const slides = useSlidesStore()
const { goPrev, goNext, total, enableNext, disableNext, enablePrev, disablePrev} = slides
const { current, prev, next } = storeToRefs(slides)

watch(current, () => {
  current.value <= 0 ? disablePrev() : enablePrev()
  current.value >= total-1 ? disableNext() : enableNext()
})

</script>

<template>
  <button class="nav-btn" id="prev" @click="goPrev" :disabled="(!prev)">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="15"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="4"
      stroke-linecap="round"
      stroke-linejoin="round"
      class="feather feather-arrow-left"
    >
      <line x1="19" y1="12" x2="5" y2="12"></line>
      <polyline points="12 19 5 12 12 5"></polyline>
    </svg>
  </button>
  <slot></slot>
  <button class="nav-btn" id="next" @click="goNext" :disabled="(!next)">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="15"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="4"
      stroke-linecap="round"
      stroke-linejoin="round"
      class="feather feather-arrow-right"
    >
      <line x1="5" y1="12" x2="19" y2="12"></line>
      <polyline points="12 5 19 12 12 19"></polyline>
    </svg>
  </button>
</template>

<style scoped lang="scss">
button {
    font-weight: bold;
    color: white;
    background-color: #1ea3de;
    height: 129px;
    border-width: 1px;
    &:disabled {
      background-color: gray;
    }
  }
</style>
