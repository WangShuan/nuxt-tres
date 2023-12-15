<template>
  <Title>Tres.js 載入 GLTF 模型方法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 300]" />
    <Suspense>
      <primitive :object="model" />
    </Suspense>
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
  <div class="btns">
    <button @click="playAction('idle')">idle</button>
    <button @click="playAction('skate')">skate</button>
    <button @click="playAction('snap')">snap</button>
    <button @click="playAction('shoot')">shoot</button>
    <button @click="playAction('rocketBoot')">rocketBoot</button>
    <button @click="playAction('groundPound')">groundPound</button>
    <button @click="playAction('dance')">dance</button>
  </div>
</template>

<script setup>
const { scene: model, animations } = await useGLTF(
  '/models/robot/multiclip.gltf',
)

model.position.y = -70

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