<template>
  <Title>Tres.js Text3D 用法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <Suspense>
      <Text3D :text="ipt" font="/fonts/FiraCodeRegular.json" center need-updates>
        <TresMeshNormalMaterial />
      </Text3D>
    </Suspense>
    <OrbitControls />

  </TresCanvas>
  <div class="input">
    <label for="ipt">Type something: </label>
    <input id="ipt" type="text" v-model="ipt">
  </div>
</template>

<script setup>
const ipt = ref('Tres.js is awesome!')
</script>

<style>
label {
  color: #fff;
}

.input {
  position: absolute;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 18px;
}

input {
  font-size: 18px;
}
</style>