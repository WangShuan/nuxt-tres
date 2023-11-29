<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 30]" />
    <Suspense>
      <TexturedMBall />
    </Suspense>
    <Suspense>
      <TexturedBall />
    </Suspense>
    <Suspense>
      <TexturedMBall2 />
    </Suspense>
    <Stars />
    <OrbitControls />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="2" cast-shadow />
  </TresCanvas>
</template>