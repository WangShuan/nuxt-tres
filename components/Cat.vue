<template>
  <primitive :object="model" />
</template>

<script setup>
const props = defineProps({
  action: { type: String }
})

const { scene: model, animations } = await useGLTF(
  '/models/little_cat/scene.gltf',
)

model.scale.x = 5
model.scale.y = 5
model.scale.z = 5
model.position.y = -1.5
const { actions } = useAnimations(animations, model)
const currentAction = ref()
const setActions = (val) => {
  if (currentAction.value) {
    currentAction.value.stop()
  }
  const name = Object.keys(actions).find(a => a.indexOf(val) != -1)
  currentAction.value = actions[name]
  currentAction.value.clampWhenFinished = true
  currentAction.value.play()
}

watch(() => props.action, (newV, oldV) => {
  setActions(newV)
});
</script>