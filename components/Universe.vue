<template>
  <TresGroup>
    <Levioso v-bind="leviosoState">
      <primitive ref="planeRef" :object="model" />
    </Levioso>
    <TresMesh v-for="(o, i) in obstacles" :key="o" :position="[o.x, o.y, o.z]" :rotate-z="o.x / 100">
      <TresBoxGeometry :args="[0.08, 0.08, 0.08]" />
      <TresMeshToonMaterial color="red" />
    </TresMesh>
    <TresMesh v-for="i in bullets" :key="i" :position="[i.x, i.y, i.z]">
      <TresBoxGeometry :args="[0.05, 0.05, 0.05]" />
      <TresMeshBasicMaterial />
    </TresMesh>
  </TresGroup>
</template>
<script setup>
// 在父層處理 gameover 畫面
const emit = defineEmits(['setGameover']);
// 載入飛機模型
const { scene: model } = await useGLTF('/models/airplane.gltf', { draco: true });
// 讓飛機稍微傾斜角度
model.rotation.set(0, Math.PI / 2, 0.3);
// 設置飛機 y 位置
model.position.y = -0.2;
// 設定讓飛機可以些微自動漂浮的效果
const leviosoState = reactive({
  speed: 10,
  rotationFactor: 0.8,
  floatFactor: 0.4,
});

const planeRef = ref();
const obstacles = ref([]);
const bullets = ref([]);
const gameover = ref(false)
const x = ref(0);
const y = ref(0);

// 生成隨機 -10 ~ 10 的數字（用來隨機產生障礙物）
function getRandomCoordinate() {
  return (Math.random() * 10 - (-5) + 1) + (-10);
}

// 生成初始的障礙物
for (let i = 0; i < 300; i++) {
  obstacles.value.push({
    x: getRandomCoordinate() + 9,
    y: getRandomCoordinate(),
    z: 0
  })
}

// 建立速率用的參數（用來讓障礙物隨時間加速移動）
const speedIncrement = 0.001;
let currentSpeed = 0.1;

const { onLoop } = useRenderLoop();

onLoop(({ delta }) => {
  // 判斷是否正在遊戲中或已結束遊戲，改變飛機的位置
  if (planeRef.value && !gameover.value) {
    planeRef.value.position.x = (x.value / window.innerWidth) * 2 - 1;
    planeRef.value.position.y = -(y.value / window.innerHeight) * 2 + 1;
  } else {
    planeRef.value.rotation.z = Math.PI
    planeRef.value.position.y -= delta
  }
  // 處理障礙物
  if (obstacles.value) {
    // 概抓飛機中心點左到右的 x 位置判斷是否撞到障礙物
    const px = [-0.2, -0.1, 0, 0.1, 0.2];
    const p = { x: planeRef.value.position.x, y: planeRef.value.position.y, z: planeRef.value.position.z };
    px.forEach(x => {
      p.x = p.x + x;
      obstacles.value.forEach((e, i) => {
        if (calculateDistance(p, e) < 0.05) {
          gameover.value = true
          emit('setGameover', true)
        }
      });
    });
    // 讓障礙物持續往 -x 方向移動
    obstacles.value.forEach((e, j) => {
      e.x -= currentSpeed * delta;
      // 超過一定範圍後將障礙物刪除（不然無限增加障礙物電腦會跑不動）
      if (e.x < -5) {
        obstacles.value.splice(j, 1);
      }
    })
  }
  // 處理子彈
  if (bullets.value.length > 0) {
    // 讓子彈一直往 x 方向移動
    bullets.value.forEach((e, i) => {
      bullets.value[i].x += delta * 2
    })

    // 判斷子彈是否有撞到障礙物，清除子彈與障礙物
    obstacles.value.forEach((e, j) => {
      bullets.value.forEach((e, i) => {
        if (calculateDistance(bullets.value[i], obstacles.value[j]) < 0.05) {
          bullets.value.splice(i, 1);
          obstacles.value.splice(j, 1);
        }
      });
    })
  }
});

// 監聽滑鼠移動與鍵盤事件
onMounted(() => {
  document.addEventListener("mousemove", handleMouseMove);
  document.addEventListener("keypress", handleKeypress)
});

// 取消監聽滑鼠移動與鍵盤事件
onUnmounted(() => {
  document.removeEventListener("mousemove", handleMouseMove);
  document.removeEventListener("keypress", handleKeypress)
})

// 滑鼠移動事件（用來改變飛機位置）
function handleMouseMove(e) {
  x.value = e.clientX
  y.value = e.clientY
}

// 鍵盤事件（用來發射子彈）
function handleKeypress(e) {
  if (e.code == 'Space') {
    bullets.value.push({
      x: planeRef.value.position.x + 0.15,
      y: planeRef.value.position.y,
      z: planeRef.value.position.z
    })
  }
}

// 設定季實際，每十秒就添加障礙物一次，並加快障礙物的移動速度
setInterval(() => {
  for (let i = 0; i < 100; i++) {
    obstacles.value.push({
      x: getRandomCoordinate() + 10,
      y: getRandomCoordinate(),
      z: 0
    })
  }
  currentSpeed += speedIncrement;
}, 10000)
</script>

<style>
.over {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  background: #ffffff70;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  color: #fff;
  z-index: 100;
}
</style>