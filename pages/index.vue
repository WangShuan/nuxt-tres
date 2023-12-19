<template>
  <Title>Nuxt3 & Tres.js Learning Collections</Title>
  <TresCanvas window-size shadows alpha clear-color="#000">
    <TresPerspectiveCamera :look-at="[0, 0, 0]" :position="[0, 20, 45]" />
    <Suspense>
      <Map @changeLight="changeLight" />
    </Suspense>
    <TresGroup :position="[25, 0, -5]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[5, 0, 0]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[15, 0, -15]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[-10, 0, -5]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[-20, 0, -15]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[-23, 0, 7]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[-12, 0, 18]">
      <Tree />
    </TresGroup>
    <TresGroup :position="[17, 0, 13]">
      <Tree />
    </TresGroup>
    <Suspense>
      <Floor />
    </Suspense>
    <Stars :rotation="[0, yRotation, 0]" :radius="50" :depth="100" :count="5000" :size="0.2" :size-attenuation="true" />
    <OrbitControls :enable-damping="true" :enable-rotate="false" :min-distance="45" :max-distance="55" :enable-pan="false" />
    <TresPointLight ref="light" :args="['white', 1, 50, 0]" :position="[0, 10, 15]" cast-shadow :shadow-radius="10" />
  </TresCanvas>
</template>

<script setup>
const yRotation = shallowRef(0)
useRenderLoop().onLoop(({ delta }) => {
  yRotation.value += 0.02 * delta
  if (close.value) {
    light.value.intensity = lerp(light.value.intensity, 0, delta * 2)
  } else {
    light.value.intensity = lerp(light.value.intensity, 2, delta * 2)
  }
})

const light = ref()
const close = ref(false)
const changeLight = () => {
  close.value = true
  setTimeout(() => {
    close.value = false
  }, 1000);
}

definePageMeta({
  layout: false
})
</script>