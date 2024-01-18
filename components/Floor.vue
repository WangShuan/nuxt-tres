<template>
  <TresMesh receive-shadow :rotate-x="-Math.PI / 2" :position="[0, -1.5, 0]">
    <TresPlaneGeometry :args="[160, 80]" />
    <TresMeshStandardMaterial v-bind="floorTexture" />
    <HtmlByCientos transform :position="[0, -25, 0]">
      <div class="description">請使用鍵盤 W、S、A、D 按鍵移動小兔子，讓牠走進你想前往的地方<br>Please use the W, S, A, D keys to move the rabbit and guide it to the destination of your choice.</div>
    </HtmlByCientos>
  </TresMesh>

  <TresMesh receive-shadow :rotate-x="-Math.PI / 2" :position="[0, -1.49, 12]">
    <TresPlaneGeometry :args="[34.6, 24]" />
    <TresMeshStandardMaterial v-bind="roadTexture" color="gold" />
  </TresMesh>
</template>

<script setup>
import { Html as HtmlByCientos } from '@tresjs/cientos';

// 引入紋理貼圖給地板使用
const floorTexture = await useTexture({
  map: '/textures/floor.jpg',
})

const roadTexture = await useTexture({
  map: '/textures/road.jpeg'
})
</script>

<style scoped>
.description {
  box-sizing: border-box;
  font-size: 24px;
  text-align: center;
  font-weight: bold;
  display: flex;
  width: 80vw;
  justify-content: center;
  align-items: center;
  color: #fff;
}
</style>