<template>
    <div class="knime-manager">
        <KnimeSearch :node-list="nodeList" />
        <KnimeCanvas />
    </div>
</template>

<script>
import { API_NODES_LIST } from "@/constants/api"
import KnimeSearch from "./KnimeSearch/"
import KnimeCanvas from "./KnimeCanvas/"

export default {
  name: 'NodeManager',
  data: function () {
      return {
          nodeList: [],
      }
  },
  created () {
      this.fetchNodes()
  },
  methods: {
      async fetchNodes () {
        // Load list of nodes using API
        const resp = await fetch(process.env.VUE_APP_API_ENDPOINT + API_NODES_LIST)
        this.nodeList = await resp.json()
      }
  },
  components: {
      KnimeCanvas,
      KnimeSearch
  }
}
</script>

<style scoped>
    .knime-manager {
        height: 100%;
        position: relative;
    }
</style>
