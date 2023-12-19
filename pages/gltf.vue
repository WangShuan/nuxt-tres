<template>
  <Title>Tres.js 載入 GLTF 模型方法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <Suspense>
      <primitive :object="model" />
    </Suspense>
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
  <div class="btns">
    <button @click="playAction('0TPose')">TPose</button>
    <button @click="playAction('Grabbed')">Grabbed</button>
    <button @click="playAction('Greeting')">Greeting</button>
    <button @click="playAction('Iddle')">Iddle</button>
  </div>
</template>

<script setup>
const { scene: model, animations } = await useGLTF(
  '/models/ugly-naked-bunny.gltf',
)

model.position.y = -2

const { actions } = useAnimations(animations, model)
const currentAction = ref()

const playAction = (name) => {
  if (currentAction.value) {
    currentAction.value.stop()
  }
  currentAction.value = actions[name]
  currentAction.value.setLoop(2500, 1)
  currentAction.value.clampWhenFinished = true
  currentAction.value.play()
}
</script>

<style>
.btns {
  position: absolute;
  bottom: 0;
  right: 0;
  display: flex;
  flex-direction: column;
}

button {
  margin: 5px;
  padding: 5px 10px;
  background: #333;
  color: #fff;
  font-size: 18px;
}
</style>