<template>
  <Title>Tres.js Texture 用法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 20]" />
    <Suspense>
      <RedMatcapBall />
    </Suspense>
    <Suspense>
      <RockMapBall />
    </Suspense>
    <Suspense>
      <WaterMatcapBall />
    </Suspense>
    <Stars :radius="2" :rotation="[0, yRotation, 0]" :count="1024" />
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
</template>

<script setup>
const yRotation = shallowRef(0)
useRenderLoop().onLoop(({ delta }) => {
  yRotation.value += 0.02 * delta
})
</script>