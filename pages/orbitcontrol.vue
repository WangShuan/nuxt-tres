<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera />
    <TresMesh :rotation="[3, 0, 5]">
      <Tetrahedron>
        <TresMeshNormalMaterial />
      </Tetrahedron>
    </TresMesh>
    <OrbitControls />
  </TresCanvas>
</template>