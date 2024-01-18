<template>
  <Title>Nuxt3 & Tres.js Learning Collections</Title>
  <TresCanvas window-size shadows alpha clear-color="#122F50">
    <TresPerspectiveCamera :look-at="[0, 0, 0]" :position="[0, 15, 45]" />
    <Suspense>
      <Map @changeLight="changeLight" />
    </Suspense>

    <TresGroup v-for="item in fences" :rotate-y="item.rotateY ? Math.PI / 2 : 0" :position="item.position">
      <Fence />
    </TresGroup>

    <template v-for="j in 5">
      <TresGroup v-for="i in 4" :rotate-y="Math.PI / i + j" :position="[1.25 + (i * 2.25), -1, 2 + j]" :scale="0.5">
        <Tree />
      </TresGroup>
      <TresGroup v-for="i in 4" :rotate-y="Math.PI / i + j" :position="[-12.25 + (i * 2.25), -1, 2 + j]" :scale="0.5">
        <Tree />
      </TresGroup>
    </template>

    <Suspense>
      <Floor />
    </Suspense>

    <TresGroup v-for="item in coulds" :key="item" :position="item">
      <Suspense>
        <Could />
      </Suspense>
    </TresGroup>

    <!-- Moon -->
    <TresMesh :position="[-5, 14, 15]" :rotate-y="-Math.PI / 2.5">
      <TresSphereGeometry :args="[2, 64, 64, Math.PI / 6, Math.PI / 3]" />
      <TresMeshStandardMaterial color="yellow" emissive-intensity="1" metalness="0.5" roughness="0.5" emissive="#cccca3" :side="2" />
    </TresMesh>

    <TresDirectionalLight ref="light" :args="['#aaaaaa', 2]" :position="[-5, 14, 15]" cast-shadow :shadow-radius="5" />
    <OrbitControls :enable-damping="true" :enable-rotate="false" :min-distance="45" :max-distance="55" :enable-pan="false" />
    <Stars :rotation="[0, yRotation, 0]" :count="300" :size="0.5" :size-attenuation="true" />
  </TresCanvas>
</template>

<script setup>
const coulds = ref([[-3, 10, -20], [15, 13, -18], [-15, 10, -6]])
const fences = ref([])
for (let i = 0; i <= 12; i++) {
  if (i <= 3) {
    fences.value.push({ position: [2, -0.5, 2 * i], rotateY: true })
    fences.value.push({ position: [-2, -0.5, 2 * i], rotateY: true })
    fences.value.push({ position: [12, -0.5, 2 * i], rotateY: true })
    fences.value.push({ position: [-12, -0.5, 2 * i], rotateY: true })
  }
  if (i <= 4) {
    fences.value.push({ position: [-3 + -2 * i, -0.5, 8], rotateY: false })
    fences.value.push({ position: [3 + 2 * i, -0.5, 8], rotateY: false })
  }
  fences.value.push({ position: [-17, -0.5, 2 * i], rotateY: true })
  fences.value.push({ position: [17, -0.5, 2 * i], rotateY: true })
}
const yRotation = shallowRef(0)
useRenderLoop().onLoop(({ delta }) => {
  yRotation.value += 0.01 * delta
  if (close.value) {
    light.value.intensity = lerp(light.value.intensity, 0, delta * 2)
  } else {
    light.value.intensity = lerp(light.value.intensity, 2, delta * 2)
  }

  light.value.shadow.camera.left = -40;
  light.value.shadow.camera.right = 40;
  light.value.shadow.camera.top = 40;
  light.value.shadow.camera.bottom = -40;

  light.value.shadow.mapSize.width = 2048;
  light.value.shadow.mapSize.height = 2048;

  light.value.shadow.bias = -0.001;
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