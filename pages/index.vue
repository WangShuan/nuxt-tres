<template>
  <Title>Tres.js 基礎使用</Title>
  <TresCanvas clear-color="#82DBC5" window-size>
    <TresPerspectiveCamera :position="[0, 0, 3]" />
    <TresMesh>
      <TresTorusGeometry :args="[0.2, 0.1, 16, 32]" />
      <TresMeshNormalMaterial />
    </TresMesh>
  </TresCanvas>
</template>
