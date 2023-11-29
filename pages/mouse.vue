<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 3]" />
    <TresMesh :rotation="[-Math.PI / 5, 0, Math.PI / 3]">
      <TresCapsuleGeometry :args="[0.2, 0.5, 4, 8]" />
      <TresMeshNormalMaterial />
    </TresMesh>
    <MouseParallax :factor="1" :ease="3" />
  </TresCanvas>
</template>