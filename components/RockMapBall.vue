<script setup>
const pbrTexture = await useTexture({
  map: '/textures/Rock035_2K_Displacement.jpg',
  displacementMap: '/textures/Rock035_2K_Displacement.jpg',
  roughnessMap: '/textures/Rock035_2K_Roughness.jpg',
  normalMap: '/textures/Rock035_2K_NormalGL.jpg',
  ambientOcclusion: '/textures/Rock035_2K_AmbientOcclusion.jpg',
})
</script>

<template>
  <TresMesh :position="[1, 3, 5]">
    <TresSphereGeometry :args="[1.2, 100, 100]" />
    <TresMeshStandardMaterial v-bind="pbrTexture" :displacement-scale="0.1" />
  </TresMesh>
</template>
