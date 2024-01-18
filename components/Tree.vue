<template>
  <TresGroup>
    <TresMesh cast-shadow>
      <TresCylinderGeometry :args="[0.2, 0.24, 3, 5]" />
      <TresMeshLambertMaterial color="#795548" />
    </TresMesh>

    <TresMesh cast-shadow :rotate-z="Math.PI / 4" :position="[-0.75, 2, 0]">
      <TresCylinderGeometry :args="[0.2, 0.24, 2, 5]" />
      <TresMeshLambertMaterial color="#795548" />
    </TresMesh>
    <TresMesh cast-shadow :position="[-1, 3.5, 0]">
      <TresSphereGeometry :args="[2, 8, 4]" />
      <TresMeshStandardMaterial color="#089000" />
    </TresMesh>

    <TresMesh cast-shadow :rotate-z="-Math.PI / 4" :position="[0.75, 2, 0]">
      <TresCylinderGeometry :args="[0.2, 0.24, 2, 5]" />
      <TresMeshLambertMaterial color="#795548" />
    </TresMesh>
    <TresMesh cast-shadow :position="[1, 3, 0]">
      <TresSphereGeometry :args="[1.5, 8, 4]" />
      <TresMeshStandardMaterial color="#089000" />
    </TresMesh>

    <TresMesh cast-shadow :rotate-z="Math.PI / 2" :position="[-0.75, 2, 0]">
      <TresCylinderGeometry :args="[0.2, 0.24, 2, 5]" />
      <TresMeshLambertMaterial color="#795548" />
    </TresMesh>
    <TresMesh cast-shadow :position="[0, 4, -1]">
      <TresSphereGeometry :args="[1.75, 8, 4]" />
      <TresMeshStandardMaterial color="#089000" />
    </TresMesh>
  </TresGroup>
</template>
