<template>
  <div id="app">
    <KnimeManager />
  </div>
</template>

<script>
import KnimeManager from "@/components/KnimeManager"

export default {
  name: 'App',
  components: {
    KnimeManager
  }
}
</script>

<style>
:root {
  --global-move-step: 14px;
  --global-node-height: calc(var(--global-move-step) * 4);
  --global-node-width: calc(var(--global-move-step) * 4);
  --global-radius: 7px;
  --global-gap-x: 10px;
  --global-gap-y: 10px;
  --global-duration-short: 0.2s;
  --global-text-sm: 15px;
  --global-text-md: 18px;
}

body, html, #app {
  height: 100%;
  padding: 0;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 18px;
}
</style>
