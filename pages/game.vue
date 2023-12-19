<template>
  <Title>Tres.js 飛機打方塊小遊戲</Title>
  <TresCanvas window-size alpha>
    <TresPerspectiveCamera :position="[0, 0, 5]" />
    <Suspense>
      <Universe @setGameover="setGameover" />
    </Suspense>
    <TresDirectionalLight :position="[0, 2, 4]" />
    <TresMesh>
      <TresBoxGeometry />
      <TresMeshStandardMaterial transparent :opacity="0" />
      <Html center transform :distance-factor="1.5" :position="[0, -2, 0]">
      <div class="description">
        請使用滑鼠控制飛機位置，並通過鍵盤空白鍵發射方塊擊落障礙物，若飛機碰到障礙物則墜機並宣告遊戲失敗！
        <br>
        Control the airplane's position using the mouse and shoot cubes to knock down obstacles with the spacebar on the keyboard. If the airplane collides with an obstacle, it will crash, and the game will be declared a failure!
      </div>

      </Html>
    </TresMesh>
    <Stars :radius="2" :count="1024" />
  </TresCanvas>

  <div class="gameover" v-if="gameover">
    GAMEOVER.
    <button class="btn" @click="reloadNuxtApp()">RESTART</button>
  </div>
</template>

<script setup>
import { Html } from '@tresjs/cientos';

const gameover = ref(false)

const setGameover = (val) => gameover.value = val

definePageMeta({
  layout: false
})
</script>

<style scoped>
.gameover {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-size: 24px;
  background: #0000007c;
  color: #fff;
}

.btn {
  background: #000;
  color: #fff;
  border: 1px solid #fff;
  border-radius: 8px;
  padding: 4px 8px;
  margin-top: 8px;
}

.description {
  box-sizing: border-box;
  font-size: 24px;
  text-align: center;
  font-weight: bold;
  display: flex;
  width: 80vw;
  justify-content: center;
  align-items: center;
  color: #fff;
}
</style>