<script setup lang="ts">
import p5 from 'p5'
import { watch } from 'vue'

const props = defineProps<{
  sketchFn: (p: p5) => void
}>()
watch(
  () => props.sketchFn,
  () => {
    requestAnimationFrame(() => {
      const sketchElement = document.getElementById('sketch')
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
  <div id="sketch"></div>
</template>
<style scoped>
#vue-canvas {
  display: block;
  margin: 0 auto;
  padding: 0;
  width: 500px;
  height: 500px;
  border-radius: 20px;
  overflow: hidden;
}
</style>
