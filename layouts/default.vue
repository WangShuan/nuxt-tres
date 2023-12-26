<template>
  <header>
    <nav>
      <NuxtLink to="/init">first scene</NuxtLink>
      <NuxtLink to="/loop">onLoop</NuxtLink>
      <NuxtLink to="/orbitcontrol">OrbitControls</NuxtLink>
      <NuxtLink to="/mouse">MouseParallax</NuxtLink>
      <NuxtLink to="/text3d">Text 3D</NuxtLink>
      <NuxtLink to="/levioso">Levioso</NuxtLink>
      <NuxtLink to="/scroll">ScrollControls</NuxtLink>
      <NuxtLink to="/texture">useLoader</NuxtLink>
      <NuxtLink to="/gltf">useGLTF</NuxtLink>
    </nav>
  </header>
  <slot />
</template>

<style scoped>
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  background: #fff;
  box-shadow: 2px 2px 15px #eee;
  z-index: 1;
}

header nav {
  display: flex;
  align-items: flex-end;
  justify-content: center;
}

header nav>a {
  display: block;
  padding: 10px;
  text-decoration: none;
  color: #666;
}

.router-link-active {
  font-weight: bold;
  background: #fff;
  color: #333;
}

.tres {
  width: 300px;
  height: 300px;
  position: fixed;
  z-index: -1;
  top: 42px !important;
}


section {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 30px;
  color: aliceblue;
}
</style>