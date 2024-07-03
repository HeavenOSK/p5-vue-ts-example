<script setup lang="ts">
import p5 from 'p5'
import { watch } from 'vue'

const props = defineProps<{
  id: string
  sketchFn: (p: p5) => void
}>()

watch(
  () => props.sketchFn,
  () => {
    requestAnimationFrame(() => {
      const sketchElement = document.getElementById(props.id)
      if (sketchElement) {
        while (sketchElement.firstChild) {
          sketchElement.removeChild(sketchElement.firstChild)
        }
      }
      new p5(props.sketchFn)
    })
  },
  {
    immediate: true
  }
)
</script>
<template>
  <div :id="id"></div>
</template>
