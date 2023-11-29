<script setup lang="ts">
const pbrTexture = await useTexture({
  map: '/textures/Rock035_2K_Displacement.jpg',
  displacementMap: '/textures/Rock035_2K_Displacement.jpg',
  roughnessMap: '/textures/Rock035_2K_Roughness.jpg',
  normalMap: '/textures/Rock035_2K_NormalGL.jpg',
  ambientOcclusion: '/textures/Rock035_2K_AmbientOcclusion.jpg',
})
</script>

<template>
  <TresMesh :position="[2, 5, 7]">
    <TresSphereGeometry :args="[1, 100, 100]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" displacement-scale="0.2" />
  </TresMesh>
</template>
