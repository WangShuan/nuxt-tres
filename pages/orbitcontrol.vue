<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera />
    <TresMesh>
      <Tetrahedron>
        <TresMeshNormalMaterial />
      </Tetrahedron>
    </TresMesh>
    <Stars />
    <!-- 添加 OrbitControls 元件 -->
    <OrbitControls />
  </TresCanvas>
</template>