<template>
  <Title>Tres.js 漂浮效果(Levioso)</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <Suspense>
      <Levioso v-bind="leviosoState">
        <Octahedron :position="[0, 0, 0]">
          <TresMeshNormalMaterial />
        </Octahedron>
      </Levioso>
    </Suspense>
  </TresCanvas>
</template>

<script setup>
const leviosoState = shallowReactive({
  speed: 5,
  rotationFactor: 1,
  floatFactor: 5
})
</script>