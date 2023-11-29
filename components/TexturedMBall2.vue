<script setup lang="ts">
const pbrTexture = await useTexture({
  matcap: '/textures/matcap-red-light.png',
})
</script>

<template>
  <TresMesh :position="[-3, -2, 9]">
    <TresSphereGeometry :args="[1, 100, 100]" />
    <TresMeshMatcapMaterial v-bind="pbrTexture" displacement-scale="0.2" />
  </TresMesh>
</template>
