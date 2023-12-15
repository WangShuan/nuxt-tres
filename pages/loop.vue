<template>
  <Title>Tres.js animate loop(onLoop)</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <TresMesh ref="boxRef">
      <TresBoxGeometry />
      <TresMeshNormalMaterial />
    </TresMesh>
  </TresCanvas>
</template>

<script setup>
const boxRef = ref()
const { onLoop } = useRenderLoop()
onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.y += delta
    boxRef.value.rotation.z = elapsed
    boxRef.value.position.y = Math.sin(elapsed * 2)
  }
})
</script>