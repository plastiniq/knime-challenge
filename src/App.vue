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

<style lang="scss">

// Bootstrap grid for responsive layout
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
@import "~bootstrap/scss/mixins";
@import "~bootstrap/scss/root";
@import "~bootstrap/scss/reboot";
@import "~bootstrap/scss/grid";

:root {
  --global-node-height: 52px;
  --global-node-width: 52px;
  --global-radius: 7px;
  --global-gap-x: 10px;
  --global-gap-y: 10px;
  --global-duration-short: 0.2s;
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
