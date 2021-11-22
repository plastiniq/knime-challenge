<template>
    <div class="knime-manager">
        <KnimeCanvas :step="step" :node-list="nodeList" />
    </div>
</template>

<script>
import { API_NODES_LIST } from "@/constants/api"
import KnimeCanvas from "./KnimeCanvas/"

export default {
    name: 'NodeManager',
    data: function () {
        return {
            nodeList: [], // All possible nodes
        }
    },
    created () {
        this.fetchNodes()
    },
    computed: {
        step() {
            // Value of CSS variable
            return parseInt(getComputedStyle(document.documentElement)
                .getPropertyValue('--global-move-step'))
        }
    },
    methods: {
        async fetchNodes () {
            // Load list of nodes using API
            const resp = await fetch(process.env.VUE_APP_API_ENDPOINT + API_NODES_LIST)
            this.nodeList = await resp.json()
        },
        
    },
    components: {
        KnimeCanvas
    }
}
</script>

<style scoped>
    .knime-manager {
        height: 100%;
        position: relative;
    }
</style>
