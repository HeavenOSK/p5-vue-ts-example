<script setup lang="ts">
import P5Sketch from '@/P5Sketch.vue'
import { ref, computed } from 'vue'

const size = ref(50)

const sketchFn = computed(() => {
  const _size = size.value
  return (p: p5) => {
    let x = 100
    let y = 100
    let xspeed = 2.5
    let yspeed = 2
    p.setup = () => {
      const canvas = p.createCanvas(640, 240)

      canvas.parent('sketch')
    }

    p.draw = () => {
      p.background(245)
      x = x + xspeed
      y = y + yspeed

      if (x > 640 || x < 0) {
        xspeed = xspeed * -1
      }
      if (y > 240 || y < 0) {
        yspeed = yspeed * -1
      }
      p.stroke(0)
      p.fill(127)
      p.circle(x, y, _size)
    }
  }
})
</script>
<template>
  <div class="flex flex-col items-center justify-center h-screen w-full gap-4">
    <P5Sketch :sketchFn="sketchFn" />
    <label class="flex items-center gap-2">
      <span class="text-gray-500">Size</span>
      <input
        class="border border-solid w-24 px-2 border-gray-400 hover:border-gray-600"
        type="number"
        v-model="size"
      />
    </label>
  </div>
</template>
