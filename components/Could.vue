<template>
  <TresMesh :position="[-1, 1, 0]">
    <TresSphereGeometry :args="[1.05, 64, 64]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" />
  </TresMesh>
  <TresMesh :position="[1, 1, 0]">
    <TresSphereGeometry :args="[1.05, 64, 64]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" />
  </TresMesh>

  <TresMesh :position="[-2, 0, 0]">
    <TresSphereGeometry :args="[1.05, 64, 64]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" />
  </TresMesh>
  <TresMesh>
    <TresSphereGeometry :args="[1.1, 64, 64]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" />
  </TresMesh>
  <TresMesh :position="[2, 0, 0]">
    <TresSphereGeometry :args="[1, 64, 64]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" />
  </TresMesh>
</template>

<script setup>
const pbrTexture = await useTexture({
  map: '/textures/could.jpeg',
})
</script>