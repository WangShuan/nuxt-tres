<template>
  <!-- 建立場景，設置 window-size 讓畫布的寬高符合視窗大小、設置 clear-color 更改場景背景顏色(預設是黑) -->
  <TresCanvas window-size>
    <!-- 建立相機，設置 :position 調整位置(預設是 3,3,3 的位置) -->
    <TresPerspectiveCamera :position="[0, 0, 10]" />
    <!-- 用 Suspense 包裹 Text3D 元件-->
    <Suspense>
      <!-- 使用 Text3D 元件，傳入文字、設定 font -->
      <Text3D text="Tres.js is awesome!" font="/fonts/FiraCodeRegular.json">
        <TresMeshNormalMaterial />
      </Text3D>
    </Suspense>
  </TresCanvas>
</template>