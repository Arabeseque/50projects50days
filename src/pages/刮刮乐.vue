<script setup lang="ts">

const el = $ref<HTMLCanvasElement>()
const ctx = $computed(() => el.getContext('2d')!)

let isDraw = false

function mouseDown() {
  isDraw = true
}
function mouseUp() {
  isDraw = false
}

function mouseMove(e: MouseEvent) {
  if (!isDraw) return
  const x = e.pageX - el.offsetLeft
  const y = e.pageY - el.offsetTop
  ctx.globalCompositeOperation = 'destination-out'
  ctx.arc(x, y, 10, 0, Math.PI * 2)
  ctx.fill()
}
onMounted(() => {
  ctx.fillStyle = 'darkgray'
  ctx.fillRect(0, 0, 400, 100)
  ctx.fillStyle = '#fff'
  ctx.fillText('刮刮卡', 180, 50)
})
</script>

<template>
  <div flex justify-center relative>
    <canvas
      ref="el"
      height="100"
      width="400"
      @mousedown="mouseDown()"
      @mouseup="mouseUp()"
      @mouseover="mouseMove($event)"
    />
    <div class="text" absolute top-45px z--1>
      刮刮卡测试
    </div>
  </div>
</template>
