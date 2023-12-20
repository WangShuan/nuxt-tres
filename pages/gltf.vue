<template>
  <Title>Tres.js 載入 GLTF 模型方法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <Suspense>
      <Cat :action="action" />
    </Suspense>
    <TresMesh receive-shadow :rotate-x="-Math.PI / 2" :position="[0, -1.5, 0]">
      <TresPlaneGeometry :args="[10, 8]" />
      <TresMeshStandardMaterial />
    </TresMesh>
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
  <div class="btns">
    <button @click="setAction('TPose')">TPose</button>
    <button @click="setAction('Idle')">Idle</button>
    <button @click="setAction('Walk')">Walk</button>
    <button @click="setAction('Run')">Run</button>
    <button @click="setAction('Jump')">Jump</button>
    <button @click="setAction('Greeting')">Greeting</button>
    <button @click="setAction('Eat')">Eat</button>
    <button @click="setAction('Sleep01')">Sleep01</button>
    <button @click="setAction('Sleep02')">Sleep02</button>
    <button @click="setAction('Sleep03')">Sleep03</button>
  </div>
</template>

<script setup>
const action = ref('TPose')

const setAction = (a) => {
  action.value = a
}
</script>

<style>
.btns {
  position: absolute;
  bottom: 0;
  right: 0;
  display: flex;
}

button {
  margin: 5px;
  padding: 5px 10px;
  background: #333;
  color: #fff;
  font-size: 18px;
}
</style>