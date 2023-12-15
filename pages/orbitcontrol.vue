<template>
  <Title>Tres.js 使用 OrbitControls</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera />
    <TresMesh :rotation="[3, 0, 5]">
      <Tetrahedron>
        <TresMeshNormalMaterial />
      </Tetrahedron>
    </TresMesh>
    <OrbitControls auto-rotate enable-damping />
  </TresCanvas>
</template>