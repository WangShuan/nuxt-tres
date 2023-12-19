<template>
  <Title>Tres.js Texture 用法</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 30]" />
    <Suspense>
      <RedMatcapBall />
    </Suspense>
    <Suspense>
      <RockMatcapBall />
    </Suspense>
    <Suspense>
      <WaterMatcapBall />
    </Suspense>
    <Stars :radius="2" :count="1024" />
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
</template>