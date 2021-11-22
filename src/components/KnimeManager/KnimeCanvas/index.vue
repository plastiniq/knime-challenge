
<template>
    <div 
        class="knime-canvas" 
        :style="{ background }"
    >
        <div class="search-container">
            <KnimeSearch :node-list="nodeList" @select="addNode" />
        </div>
        <KnimeNode 
            v-for="(node, index) in nodes" 
            :key="index + node.id" 
            :value="node"
            @mousedown.native="dragStart(node, $event)"
        />
    </div>
</template>

<script>
import KnimeNode from "../KnimeNode/"
import KnimeSearch from "../KnimeSearch/"

export default {
    name: 'KnimeCanvas',
    props: {
        nodeList: { type: Array, default: () => [] }, // All possible nodes
        step: { type: Number, default: 20 },
    },
    data: function () {
        return {
            nodes: [], // Nodes added to the canves
            dragNodeOffset: {x: 0, y: 0} // Position of the cursor within node coordinates
        }
    },
    computed: {
        background() {
            // Generate repeating check
            return `url("data:image/svg+xml,%3Csvg width='${this.step}' height='${this.step}' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0,0L0,${this.step}L${this.step},${this.step}' stroke='%23F0F0F0'/%3E%3C/svg%3E%0A") repeat left top`
        }
    },
    destroyed() {
        // Remove event listeners if exist
        this.endDrag()
    },
    methods: {
        addNode(node) {
            // Adds selected node to the canvas
            this.nodes.push(Object.assign({}, node))
        },
        dragStart(node, event) {
            this.dragNode = node

            // Coordinates to calculate offset
            const {left, top} = event.target.getBoundingClientRect()
            this.dragNodeOffset = { x: left - event.clientX, y: top - event.clientY  }

            document.addEventListener('mousemove', this.moveHandler)
            document.addEventListener('mouseup', this.endDrag)
        },
        moveHandler (e) {
            this.$set(this.dragNode, 'position', { 
                left: Math.round((e.clientX + this.dragNodeOffset.x) / this.step) * this.step , // Move by step
                top: Math.round((e.clientY + this.dragNodeOffset.y) / this.step) * this.step 
            })
        },
        endDrag() {
            document.removeEventListener('mousemove', this.moveHandler)
            document.removeEventListener('mouseup', this.endDrag)
        }
    },
    components: {
        KnimeNode,
        KnimeSearch
    }
}
</script>

<style scoped>
    .knime-canvas {
        width: 100%;
        height: 100%;
        display: flex;
        flex-flow: row wrap;
        align-content: flex-start;
    }

    .search-container {
        flex-grow: 1;
        flex-shrink: 0;
        height: var(--global-node-height);
        overflow: visible;
        z-index: 1;
        width: calc(100% - var(--global-move-step) * 2)
    }

    .knime-canvas > * {
        margin: var(--global-move-step);
    }
</style>
