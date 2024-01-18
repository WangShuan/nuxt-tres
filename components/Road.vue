<template>
  <TresMesh receive-shadow :rotate-x="-Math.PI / 2" :position="[0, -1.49, 12]">
    <TresPlaneGeometry :args="[34.6, 24]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" color="gold" />
  </TresMesh>
</template>

<script setup>
const pbrTexture = await useTexture({
  map: '/textures/road.jpeg'
})
</script>