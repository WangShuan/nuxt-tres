<template>
  <Title>Tres.js 基礎使用</Title>
  <TresCanvas window-size alpha shadows>
    <TresPerspectiveCamera :look-at="[0, 0, 0]" :position="[-10, 5, 15]" />
    <TresGroup :position="[0, 2, 0]">
      <TresMesh cast-shadow>
        <TresTorusGeometry :args="[1, 0.4, 32, 32]" />
        <TresMeshStandardMaterial color="white" />
      </TresMesh>
      <TresMesh :position="[4, 0, 0]" cast-shadow>
        <TresBoxGeometry :args="[2, 2, 2]" />
        <TresMeshStandardMaterial color="white" />
      </TresMesh>
      <TresMesh :position="[-4, 0, 0]" cast-shadow>
        <TresTorusKnotGeometry :args="[1, 0.4, 32, 32]" />
        <TresMeshStandardMaterial color="white" :roughness="0.1" />
      </TresMesh>
    </TresGroup>
    <TresMesh :rotate-x="-Math.PI / 2" receive-shadow>
      <TresPlaneGeometry :args="[15, 15]" />
      <TresMeshStandardMaterial color="white" />
    </TresMesh>
    <OrbitControls />
    <TresDirectionalLight cast-shadow ref="lightRef" :position="[5, 5, 5]" :args="['white', 1]" />
    <TresDirectionalLightHelper v-if="lightRef" :args="[lightRef, 1]" />
  </TresCanvas>
</template>

<script setup>
const lightRef = ref()
</script>