<script setup>
import { useSlidesStore } from '../stores/slides'
import { onBeforeMount, ref } from 'vue'

import SlideTerms from '@/components/SlideTerms.vue'
import SlideTermButton from '@/components/SlideTermButton.vue'

const buttons = ref([
  { id: 1, termName: 'Journal Voucher Workflow Maintainer' },
  { id: 2, termName: 'Journal Voucher Processor' },
  { id: 3, termName: 'Journal Voucher Reviewer' },
  { id: 4, termName: 'Journal Voucher Approver' },
  { id: 5, termName: 'Journal Voucher Master Processor' }
])

let terms = [
  'The Journal Voucher Workflow Maintainer loads the two tables. One table stores the user IDs of Journal Voucher Processors and the related organizations. The other table stores the user IDs of the Journal Voucher Reviewers and the Journal Voucher Approvers, and maintains the dollar thresholds for routing. GFEBS will route JVs automatically to their appropriate reviewers based on the organization from the JV originate, and to approvers based on the dollar amount of the JV.',
  'The Journal Voucher Processor prepares and parks JV.',
  'The Journal Voucher Reviewer reviews parked JVs and releases or rejects the JV. If the Journal Voucher Reviewer releases a JV, he/she sends it on the Journal Voucher Approver for final approval.',
  'The Journal Voucher Approver approves or rejects JV and processes JV documents.',
  'The Journal Voucher Master Processor uploads JVs into GFEBS and updates funding changes on purchase orders (POs)'
]

const activeDef = ref('')
const activeName = ref('')

function PassNameAndDef(name, def) {
  return (activeName.value = name), (activeDef.value = def)
}

const slideData = {
  title: 'Terms and Definition Slide',
  type: 'content',
  section: 'Section 1: What to Expect'
}

const slides = useSlidesStore()
const { addSlide } = slides

onBeforeMount(() => {
  addSlide(slideData, 6)
})
</script>

<template>
  <SlideTerms :defName="activeName" :defParagraph="activeDef" v-bind="slideData">
    <template #main-text>
      <p>Here are a number key terms and concepts related to this section.</p>
      <p><span style="font-weight: bold">Click</span> each term to the right to learn more.</p>
    </template>
    <SlideTermButton
      v-for="button in buttons"
      :key="button.id"
      :termName="button.termName"
      @click="PassNameAndDef(button.termName, terms[button.id - 1])"
      :activeName="activeName"
    ></SlideTermButton>
  </SlideTerms>
</template>

<style scoped></style>
