<template>
  <TresMesh cast-shadow :position="[10, 1.6, 10]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[14, 1.6, 10]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[12, 4.55, 10]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[4, 0.3, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresGroup ref="tresjsHomeDoor" :position="[14, 1.5, 10]">
    <TresMesh cast-shadow :position="[-3.4, 0, 0]">
      <TresSphereGeometry :position="[0, 0, 0]" :args="[0.3, 64, 64]" />
      <TresMeshStandardMaterial color="white" />
    </TresMesh>
    <TresMesh cast-shadow :position="[-2, 0, 0]">
      <TresBoxGeometry :position="[0, 1, 0]" :args="[4, 6, 0.2]" />
      <TresMeshStandardMaterial transparent opacity="1" color="black" />
      <Html transform :distance-factor="4" :position="[0, 1, 0]" :scale="[0.75, 0.75, 0.75]">
      <div class="title">@tresjs/nuxt<br>Learning Demo</div>

      </Html>
    </TresMesh>
  </TresGroup>

  <TresMesh cast-shadow :position="[-2, 1.6, 0]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[2, 1.6, 0]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[0, 4.55, 0]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[4, 0.3, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresGroup ref="tresjsLearningNote" :position="[2, 1.5, 0]">
    <TresMesh cast-shadow :position="[-3.4, 0, 0]">
      <TresSphereGeometry :position="[0, 0, 0]" :args="[0.3, 64, 64]" />
      <TresMeshStandardMaterial color="white" />
    </TresMesh>
    <TresMesh cast-shadow :position="[-2, 0, 0]">
      <TresBoxGeometry :position="[0, 0, 0]" :args="[4, 6, 0.2]" />
      <TresMeshLambertMaterial transparent opacity="1" color="#82DBC5" />
      <Html transform :distance-factor="4" :position="[0, 1, 0]" :scale="[0.75, 0.75, 0.75]">
      <div class="title">@tresjs/nuxt<br>Learning Notes</div>

      </Html>
    </TresMesh>
  </TresGroup>

  <TresMesh cast-shadow :position="[-19, 1.6, 5]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[-15, 1.6, 5]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[0.3, 6.2, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresMesh cast-shadow :position="[-17, 4.55, 5]">
    <TresBoxGeometry :position="[0, 1, 0]" :args="[4, 0.3, 0.3]" />
    <TresMeshStandardMaterial color="white" />
  </TresMesh>
  <TresGroup ref="tresjsShootingGame" :position="[-15, 1.5, 5]">
    <TresMesh cast-shadow :position="[-3.4, 0, 0]">
      <TresSphereGeometry :position="[0, 0, 0]" :args="[0.3, 64, 64]" />
      <TresMeshStandardMaterial color="white" />
    </TresMesh>
    <TresMesh cast-shadow :position="[-2, 0, 0]">
      <TresBoxGeometry :position="[0, 1, 0]" :args="[4, 6, 0.2]" />
      <TresMeshStandardMaterial transparent opacity="1" color="yellow" />
      <Html transform :distance-factor="4" :position="[0, 1, 0]" :scale="[0.75, 0.75, 0.75]">
      <div class="title">Tres.js Shooting Game</div>

      </Html>
    </TresMesh>
  </TresGroup>

  <primitive ref="p1" :object="model" />
</template>

<script setup>
import { Html } from '@tresjs/cientos'

// 調用父層改變燈光的事件（當模型走進門時觸發事件）
const emit = defineEmits(['changeLight']);

// 載入兔子模型
const { scene: model, animations, nodes } = await useGLTF('/models/ugly-naked-bunny.gltf', { draco: true })
// 設置兔子位置
model.position.y = -1.5
// 遍歷 nodes 開啟模型的陰影
for (let n in nodes) {
  nodes[n].castShadow = true
}
// 獲取兔子的動畫
const { actions } = useAnimations(animations, model)
const currentAction = ref()
const playAction = () => {
  if (currentAction.value) {
    currentAction.value.stop()
  }
  currentAction.value = actions['Grabbed']
  currentAction.value.setLoop(2500, 1)
  currentAction.value.clampWhenFinished = true
  currentAction.value.play()
}

const p1 = ref()
const tresjsHomeDoor = ref()
const tresjsLearningNote = ref()
const tresjsShootingGame = ref()
const x = ref(0)
const z = ref(18)
const r = ref(Math.PI)
const hasOpen = ref(false)

const { onLoop } = useRenderLoop();
onLoop(() => {
  if (p1.value) {
    // 讓模型按照移動方向改變面向位置
    p1.value.rotation.y = r.value
    // 讓模型按照移動方向改變位置
    p1.value.position.x = x.value
    p1.value.position.z = z.value
    // 判斷模型是否走到門裡，執行開門的動畫並另開視窗進入網頁
    if (tresjsHomeDoor.value) {
      const p = { x: tresjsHomeDoor.value.position.x - 2, y: tresjsHomeDoor.value.position.y, z: tresjsHomeDoor.value.position.z }
      if (calculateDistance(p1.value.position, p) <= 3) {
        if (!hasOpen.value) {
          hasOpen.value = true
          emit('changeLight')
          setTimeout(() => {
            navigateTo('/init', {
              external: true,
              open: {
                target: '_blank'
              }
            })
          }, 800)
        } else {
          if (tresjsHomeDoor.value.rotation.y > -Math.PI / 2) {
            tresjsHomeDoor.value.rotation.y = lerp(tresjsHomeDoor.value.rotation.y, -Math.PI / 2, 0.1);
          }
        }
      } else {
        tresjsHomeDoor.value.rotation.y = lerp(tresjsHomeDoor.value.rotation.y, 0, 0.1);
      }
    }
    if (tresjsLearningNote.value) {
      const p = { x: tresjsLearningNote.value.position.x - 2, y: tresjsLearningNote.value.position.y, z: tresjsLearningNote.value.position.z }
      if (calculateDistance(p1.value.position, p) <= 3) {
        if (!hasOpen.value) {
          hasOpen.value = true
          emit('changeLight')
          setTimeout(() => {
            navigateTo('https://hackmd.io/ghEdo63YQmCFJQg_Btw4-Q', {
              external: true,
              open: {
                target: '_blank'
              }
            })
          }, 800)
        } else {
          if (tresjsLearningNote.value.rotation.y > -Math.PI / 2) {
            tresjsLearningNote.value.rotation.y = lerp(tresjsLearningNote.value.rotation.y, -Math.PI / 2, 0.1);
          }
        }
      } else {
        tresjsLearningNote.value.rotation.y = lerp(tresjsLearningNote.value.rotation.y, 0, 0.1);
      }
    }
    if (tresjsShootingGame.value) {
      const p = { x: tresjsShootingGame.value.position.x - 2, y: tresjsShootingGame.value.position.y, z: tresjsShootingGame.value.position.z }
      if (calculateDistance(p1.value.position, p) <= 3) {
        if (!hasOpen.value) {
          hasOpen.value = true
          emit('changeLight')
          setTimeout(() => {
            navigateTo('/game', {
              external: true,
              open: {
                target: '_blank'
              }
            })
          }, 800)
        } else {
          if (tresjsShootingGame.value.rotation.y > -Math.PI / 2) {
            tresjsShootingGame.value.rotation.y = lerp(tresjsShootingGame.value.rotation.y, -Math.PI / 2, 0.1);
          }
        }
      } else {
        tresjsShootingGame.value.rotation.y = lerp(tresjsShootingGame.value.rotation.y, 0, 0.1);
      }
    }
  }
})

onMounted(() => document.addEventListener('keypress', setP1))
onUnmounted(() => document.removeEventListener('keypress', setP1))

// 讓模型根據鍵盤 W、S、A、D 移動並顯示走路的動畫
function setP1(e) {
  if (e.code === 'KeyW') {
    z.value -= 1
    r.value = Math.PI
    playAction()
    hasOpen.value = false
  }
  if (e.code === 'KeyS') {
    z.value += 1
    r.value = 0
    playAction()
    hasOpen.value = false
  }
  if (e.code === 'KeyA') {
    x.value -= 1
    r.value = -Math.PI / 2
    playAction()
    hasOpen.value = false
  }
  if (e.code === 'KeyD') {
    x.value += 1
    r.value = Math.PI / 2
    playAction()
    hasOpen.value = false
  }
}
</script>

<style>
.title {
  font-size: 64px;
  text-align: center;
  font-weight: bold;
  width: 400px;
  height: 800px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}
</style>