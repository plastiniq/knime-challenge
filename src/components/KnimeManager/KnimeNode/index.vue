
<template>
    <svg 
        class="knime-node" 
        :style="{ 
            transform: translateValue,
            position: value.position ? 'absolute' : 'relative' 
        }"
    >
        <rect 
            width="100%" 
            height="100%" 
            :fill="value.color" 
            :rx="radius"
            :ry="radius"
        /> 
    </svg>
</template>

<script>


export default {
    name: 'KnimeNode',
    props: {
        value: { type: Object, default: () => ({}) },
    },
    data: function () {
        return {}
    },
    computed: {
        radius() {
            return parseInt(getComputedStyle(document.documentElement)
                .getPropertyValue('--global-radius'))
        },
        translateValue() {
            return `translate(${this.value?.position?.left || 0}px, ${this.value?.position?.top || 0}px)`
        }
    }
}
</script>

<style scoped>
    .knime-node {
        width: var(--global-node-width);
        height: var(--global-node-width);
        left: 0;
        top: 0;
    }
</style>
