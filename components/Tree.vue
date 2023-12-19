<template>
  <TresMesh cast-shadow>
    <TresCylinderGeometry :args="[0.3, 0.5, 3, 10]" />
    <TresMeshLambertMaterial color="orange" />
  </TresMesh>
  <TresMesh cast-shadow :position="[0, 3, 0]">
    <TresSphereGeometry :args="[2, 10, 64]" />
    <TresMeshLambertMaterial color="green" />
  </TresMesh>
</template>