<template>
  <TresGroup>
    <Box :args="[0.2, 0.2, 2]" :rotate-y="Math.PI / 2" :position="[0, 0, 0]">
      <TresMeshStandardMaterial color="#f3ce96" />
    </Box>

    <TresMesh cast-shadow :position="[0, 0, 0]">
      <TresCylinderGeometry :args="[0.1, 0.1, 2, 10]" />
      <TresMeshLambertMaterial color="#f3ce96" />
    </TresMesh>
  </TresGroup>
</template>
