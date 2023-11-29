<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 3]" />
    <TresMesh ref="boxRef">
      <TresBoxGeometry />
      <TresMeshNormalMaterial />
    </TresMesh>
  </TresCanvas>
</template>

<script setup lang="ts">
const boxRef = ref()
const { onLoop } = useRenderLoop()
onLoop(() => {
  if (boxRef.value) {
    boxRef.value.rotation.y += 0.02
    boxRef.value.rotation.z += 0.01
  }
})
</script>