<template>
  <TresGroup>
    <Levioso v-bind="leviosoState">
      <KeyboardControls>
        <primitive ref="planeRef" :object="model" />
      </KeyboardControls>
    </Levioso>
    <TresMesh v-for="i in arr" :key="i" :position="[i.x, i.y, i.z]">
      <TresBoxGeometry :args="[0.05, 0.05, 0.05]" />
      <TresMeshNormalMaterial />
    </TresMesh>
    <TresMesh v-for="i in balls" :key="i" :position="[i.x, i.y, i.z]">
      <TresBoxGeometry :args="[0.05, 0.05, 0.05]" />
      <TresMeshBasicMaterial />
    </TresMesh>
    <TresMesh ref="ballRef" :position="[0, -2, 0]">
      <TresSphereGeometry :args="[1.2, 100, 100]" />
      <TresMeshStandardMaterial v-bind="pbrTexture" :displacement-scale="0.1" />
    </TresMesh>
  </TresGroup>
</template>
<script setup>
const pbrTexture = await useTexture({
  map: '/textures/Rock035_2K_Displacement.jpg',
  displacementMap: '/textures/Rock035_2K_Displacement.jpg',
  roughnessMap: '/textures/Rock035_2K_Roughness.jpg',
  normalMap: '/textures/Rock035_2K_NormalGL.jpg',
  ambientOcclusion: '/textures/Rock035_2K_AmbientOcclusion.jpg',
})

const ballRef = ref();
const planeRef = ref();
const arr = ref([]);
const balls = ref([]);
const gameover = ref(false)
const x = ref(0);
const y = ref(0);

for (let i = 0; i < 300; i++) {
  arr.value.push({
    x: (Math.random() * 10 - (-5) + 1) + (-10) + 6,
    y: (Math.random() * 10 - (-5) + 1) + (-10),
    z: 0
  })
}

const leviosoState = reactive({
  speed: 10,
  rotationFactor: 0.8,
  floatFactor: 0.4,
});

const { scene: model } = await useGLTF('/models/airplane.gltf', { draco: true });
model.rotation.set(0, Math.PI / 2, 0.3);
model.position.y = -0.2;

function calculateDistance(point1, point2) {
  const dx = point2.x - point1.x;
  const dy = point2.y - point1.y;
  const dz = point2.z - point1.z;

  return Math.sqrt(dx * dx + dy * dy + dz * dz);
}

const { onLoop } = useRenderLoop();

onLoop(({ delta }) => {
  if (planeRef.value && !gameover.value) {
    planeRef.value.position.x = (x.value / window.innerWidth) * 2 - 1;
    planeRef.value.position.y = -(y.value / window.innerHeight) * 2 + 1;
  } else {
    planeRef.value.rotation.z = Math.PI
    planeRef.value.position.y -= delta
  }
  if (ballRef.value) {
    ballRef.value.rotation.z += delta / 5;
  }
  if (arr.value) {
    const px = [-0.2, -0.1, 0, 0.1, 0.2];
    let p = { x: planeRef.value.position.x, y: planeRef.value.position.y, z: planeRef.value.position.z };
    px.forEach(x => {
      p.x = planeRef.value.position.x + x;
      arr.value.forEach((e, i) => {
        arr.value[i].x -= delta / 20;
        if (calculateDistance(p, arr.value[i]) < 0.05) {
          gameover.value = true
        }
      });
    });
  }
  if (balls.value.length > 0) {
    balls.value.forEach((e, i) => {
      balls.value[i].x += delta
    })

    arr.value.forEach((e, j) => {
      balls.value.forEach((e, i) => {
        if (calculateDistance(balls.value[i], arr.value[j]) < 0.05) {
          balls.value.splice(i, 1);
          arr.value.splice(j, 1);
        }
      });
    })
  }
});

onMounted(() => {
  document.addEventListener("mousemove", handleMouseMove);
  document.addEventListener("keypress", handleKeypress)
});

function handleMouseMove(e) {
  x.value = e.clientX
  y.value = e.clientY
}

function handleKeypress(e) {
  if (e.code == 'Space') {
    balls.value.push({
      x: planeRef.value.position.x + 0.15,
      y: planeRef.value.position.y,
      z: planeRef.value.position.z
    })
  }
}
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