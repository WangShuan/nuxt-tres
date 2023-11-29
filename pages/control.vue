<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera />
    <TresMesh>
      <TetrahedronGeometry />
      <TresMeshNormalMaterial />
    </TresMesh>
    <Stars />
    <!-- 添加 OrbitControls 元件 -->
    <OrbitControls />
  </TresCanvas>
</template>