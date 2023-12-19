<template>
  <Title>Tres.js 滾動控制 animate loop(ScrollControls)</Title>
  <div class="tres">
    <TresCanvas class="tres">
      <TresPerspectiveCamera :position="[0, 0, 4]" />
      <ScrollControls html-scroll v-model="progress">
        <TresMesh ref="groupRef">
          <Icosahedron :position="[0, 0, 0]">
            <TresMeshNormalMaterial />
          </Icosahedron>
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
const groupRef = ref()
const progress = ref(0)
const { onLoop } = useRenderLoop()
onLoop(() => {
  if (groupRef.value) {
    groupRef.value.rotation.x = progress.value * 3
    groupRef.value.rotation.y = progress.value * 3
    groupRef.value.rotation.z = progress.value * 3
  }
})
</script>

<style scoped>
.tres {
  width: 300px;
  height: 300px;
  position: fixed;
  left: 0;
  top: 0;
  z-index: -1;
}

main {
  color: #fff;
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