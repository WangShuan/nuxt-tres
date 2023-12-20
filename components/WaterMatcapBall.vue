<script setup lang="ts">
const pbrTexture = await useTexture({
  matcap: '/textures/m.jpg',
})
</script>

<template>
  <TresMesh :position="[5, -6, 3]">
    <TresSphereGeometry :args="[1, 100, 100]" />
    <TresMeshMatcapMaterial v-bind="pbrTexture" />
  </TresMesh>
</template>
