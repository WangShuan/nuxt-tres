<template>
  <NuxtLayout>
    <NuxtPage :key="$route.fullPath" />
  </NuxtLayout>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}

body {
  background: #000;
}
</style>