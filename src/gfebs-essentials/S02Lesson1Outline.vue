<script setup>
import { useSlidesStore } from '../stores/slides'
import { onBeforeMount } from 'vue'
import slide01 from '../assets/img/essentials-introduction-slide01-multiple.svg'

const slideData = {
  title: 'Lesson 1 Outline',
  type: 'content',
  img: slide01
}

const slides = useSlidesStore()
const { addSlide } = slides

onBeforeMount(() => {
  addSlide(slideData, 1)
})
</script>

<template>
  <SlideContent v-bind="slideData" :columns="1">
    <p>
      In this lesson, we're going to cover what you need to get started learning GFEBS. 
    </p>
    <p>The lesson is divided into three sections</p>
    <ol>
      <li>What to Expect</li>
      <li>Key Concepts</li>
      <li>Key Features</li>
    </ol>
    <p>First, we'll cover some basic course information</p>
  </SlideContent>
</template>

<style scoped lang="scss">

</style>
../../stores/slides