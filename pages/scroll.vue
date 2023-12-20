<template>
  <Title>Tres.js 滾動控制 animate loop(ScrollControls)</Title>
  <div class="tres">
    <TresCanvas alpha :clear-color="false" class="tres">
      <TresPerspectiveCamera :position="[0, 0, 4]" />
      <ScrollControls html-scroll v-model="progress">
        <TresMesh ref="IcosahedronRef">
          <Box :position="[-1, 0, 0]">
            <TresMeshNormalMaterial />
          </Box>
        </TresMesh>
      </ScrollControls>
    </TresCanvas>
  </div>
  <main>
    <section>
      <h1>01 Section</h1>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam, repellendus ullam. Ut maxime, ullam natus officiis sint veritatis sed autem? Esse voluptas beatae rem, modi eos molestias ea at ex!</p>
    </section>
    <section>
      <h1>02 Section</h1>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam, repellendus ullam. Ut maxime, ullam natus officiis sint veritatis sed autem? Esse voluptas beatae rem, modi eos molestias ea at ex!</p>
    </section>
    <section>
      <h1>03 Section</h1>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam, repellendus ullam. Ut maxime, ullam natus officiis sint veritatis sed autem? Esse voluptas beatae rem, modi eos molestias ea at ex!</p>
    </section>
  </main>
</template>

<script setup>
const IcosahedronRef = ref()
const progress = ref(0)
const { onLoop } = useRenderLoop()
onLoop(({ delta }) => {
  IcosahedronRef.value.rotation.z += delta * 2
  if (IcosahedronRef.value) {
    IcosahedronRef.value.rotation.x = progress.value * 10
    IcosahedronRef.value.rotation.y = progress.value * 10
    IcosahedronRef.value.scale.x = progress.value - 0.5
    IcosahedronRef.value.scale.y = progress.value - 0.5
    IcosahedronRef.value.scale.z = progress.value - 0.5
    IcosahedronRef.value.position.x = (progress.value - 0.5) * 5
    IcosahedronRef.value.position.y = (progress.value - 0.5) * -2
    IcosahedronRef.value.position.z = progress.value - 0.5
  }
})
</script>

<style scoped>
.tres {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  z-index: -1;
}

section {
  height: 100vh;
  border: 1px solid green;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 30px;
}
</style>