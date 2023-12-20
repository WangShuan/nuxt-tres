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
</style>