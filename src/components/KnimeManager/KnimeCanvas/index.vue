
<template>
    <div class="knime-canvas" :style="background"></div>
</template>

<script>

export default {
    name: 'KnimeCanvas',
    props: {
        nodeList: { type: Array, default: () => [] },
        step: { type: Number, default: 20 }
    },
    data: function () {
        return {}
    },
    computed: {
        background() {
            // Generate repeating check
            return { background: `url("data:image/svg+xml,%3Csvg width='${this.step}' height='${this.step}' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M0,0L0,${this.step}L${this.step},${this.step}' stroke='%23F0F0F0'/%3E%3C/svg%3E%0A") repeat left top`}
        }
    },
    created () {
        console.log(this.background)
    },
    methods: {
    }
}
</script>

<style scoped>
    .knime-canvas {
        width: 100%;
        height: 100%;
    }
</style>
