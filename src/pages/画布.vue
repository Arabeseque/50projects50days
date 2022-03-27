<script setup lang="ts">

const el = $ref<HTMLCanvasElement>()
const ctx = $computed(() => el.getContext('2d')!)

const color = ref('#fff')
useStorage('color', color)
const type = ref('rect')

const isDraw = ref(false)
function changeType(drawType: string) {
  type.value = drawType
}
const startX = ref(0)
const startY = ref(0)
function canvasDown(e: MouseEvent) {
  isDraw.value = true
  startX.value = e.pageX - el.offsetLeft
  startY.value = e.pageY - el.offsetTop
}

const imageData = ref()
function canvasUp() {
  isDraw.value = false
  imageData.value = ctx.getImageData(0, 0, el.width, el.height)
}

function canvasMove(e: MouseEvent) {
  if (!isDraw.value) return
  const x = e.pageX - el.offsetLeft
  const y = e.pageY - el.offsetTop
  if (type.value === 'rect') {
    ctx.clearRect(0, 0, 800, 400)
    imageData.value && ctx.putImageData(imageData.value, 0, 0, 0, 0, 800, 400)
    ctx.beginPath()
    ctx.strokeStyle = color.value
    ctx.rect(startX.value, startY.value, x - startX.value, y - startY.value)
    ctx.stroke()
    ctx.closePath()
  }
  else if (type.value === 'huabi') {
    ctx.beginPath()
    ctx.arc(x, y, 5, 0, 2 * Math.PI)
    ctx.fillStyle = color.value
    ctx.fill()
    ctx.closePath()
  }
  else if (type.value === 'circle') {
    isDraw.value && ctx.clearRect(0, 0, 800, 400)
    imageData.value && ctx.putImageData(imageData.value, 0, 0, 0, 0, 800, 400)
    ctx.beginPath()
    ctx.strokeStyle = color.value
    ctx.arc(startX.value, startY.value, Math.round(
      Math.sqrt((x - startX.value) * (x - startX.value) + (y - startY.value) * (y - startY.value)),
    ), 0, 2 * Math.PI)
    ctx.stroke()
    ctx.closePath()
  }
}

function clear() {
  imageData.value = null
  ctx.clearRect(0, 0, 800, 400)
}

function saveImg() {
  const img = new Image()
  img.src = el.toDataURL('image/png')
  img.onload = () => {
    const a = document.createElement('a')
    a.href = img.src
    a.download = 'canvas.png'
    a.click()
  }
}

onMounted(() => {
  el.addEventListener('mousedown', canvasDown)
  el.addEventListener('mousemove', canvasMove)
  el.addEventListener('mouseup', canvasUp)
  el.addEventListener('mouseout', canvasUp)
})

</script>

<template>
  <div flex items-center justify-center mb-8px>
    <el-button color="#626aef" plain @click="changeType('huabi')">
      画笔
    </el-button>
    <el-button color="#626aef" plain @click="changeType('rect')">
      正方形
    </el-button>
    <el-button color="#626aef" plain @click="changeType('circle')">
      圆形
    </el-button>
    <div m-8px>
      颜色:
    </div>
    <el-color-picker v-model="color" />
    <el-button color="#626aef" plain @click="clear()">
      清空
    </el-button>
    <el-button color="#626aef" plain @click="saveImg()">
      保存
    </el-button>
  </div>
  <div flex justify-center>
    <canvas ref="el" width="800" height="400" border />
  </div>
</template>
