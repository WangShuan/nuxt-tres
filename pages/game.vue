<template>
  <Title>Tres.js 飛機打方塊小遊戲</Title>
  <TresCanvas window-size>
    <TresPerspectiveCamera :position="[0, 0, 3]" />
    <Suspense>
      <Universe />
    </Suspense>
    <TresDirectionalLight :position="[0, 2, 4]" />
    <Stars :radius="2" :count="1024" />
    <OrbitControls />
  </TresCanvas>
</template>

<script setup>
onMounted(() => alert('請使用滑鼠控制飛機位置，並通過鍵盤空白鍵發射方塊擊落障礙物，若飛機撞到障礙物將會墜機！'))
</script>