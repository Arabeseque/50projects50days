<script setup lang="ts">

const el = $ref<HTMLCanvasElement>()
const ctx = $computed(() => el.getContext('2d')!)

function drawLine(lineBegin: number, lineEnd: number, lineStyle?: string) {
  ctx.beginPath()
  // moveTo设置画线起点
  ctx.moveTo(lineBegin, 0)
  // lineTo设置画线经过点
  ctx.lineTo(lineEnd, 0)
  ctx.lineWidth = 10
  ctx.strokeStyle = lineStyle || '#000'
  ctx.stroke()
  ctx.closePath()
  ctx.restore()
  ctx.save()
}
function logic() {
  ctx.save()
  ctx.clearRect(0, 0, 600, 600)
  ctx.translate(300, 300)
  ctx.save()

  // 画大圆
  ctx.beginPath()
  // 画圆线使用arc(中心点X,中心点Y,半径,起始角度,结束角度)
  ctx.arc(0, 0, 100, 0, 2 * Math.PI)
  ctx.stroke() // 执行画线段的操作
  ctx.closePath()

  // 画小圆
  ctx.beginPath()
  ctx.arc(0, 0, 5, 0, 2 * Math.PI)
  ctx.stroke()
  ctx.closePath()

  // 获取当前 时，分，秒
  const time = new Date()
  const hour = time.getHours()
  const min = time.getMinutes()
  const sec = time.getSeconds()

  // 画时针
  ctx.rotate(hour / 12 * 2 * Math.PI * 2 + 2 * Math.PI / 12 / 60 * min - Math.PI / 2)
  drawLine(-10, 50)

  // 画分针
  ctx.rotate(min / 60 * 2 * Math.PI + 2 * Math.PI / 60 / 60 * sec - Math.PI / 2)
  drawLine(-10, 60, 'skyblue')

  // 画秒针
  ctx.rotate(sec / 60 * 2 * Math.PI - Math.PI / 2)
  drawLine(-10, 80, 'pink')

  // 绘制刻度，也是跟绘制时分秒针一样，只不过刻度是死的
  ctx.lineWidth = 1
  for (let i = 0; i < 60; i++) {
    ctx.rotate(2 * Math.PI / 60)
    ctx.beginPath()
    ctx.moveTo(90, 0)
    ctx.lineTo(100, 0)
    // ctx.strokeStyle = 'red'
    ctx.stroke()
    ctx.closePath()
  }
  ctx.restore()
  ctx.save()
  ctx.lineWidth = 5
  for (let i = 0; i < 12; i++) {
    ctx.rotate(2 * Math.PI / 12)
    ctx.beginPath()
    ctx.moveTo(85, 0)
    ctx.lineTo(100, 0)
    ctx.stroke()
    ctx.closePath()
  }

  ctx.restore()
  ctx.restore()
}
function init() {
  setInterval(() => {
    logic()
  }, 1000)
}
onMounted(() => {
  init()
})
</script>

<template>
  <canvas ref="el" width="600" height="600" border />
</template>
