<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 3]" />
    <TresMesh>
      <TresTorusGeometry :args="[0.2, 0.1, 16, 32]" />
      <TresMeshNormalMaterial color="orange" />
    </TresMesh>
  </TresCanvas>
</template>
