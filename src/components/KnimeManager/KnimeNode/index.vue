
<template>
    <div class="knime-node" :style="{ backgroundColor: this.value.color }"></div>
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
    }
}
</script>

<style scoped>
    .knime-node {
        width: var(--global-node-width);
        height: var(--global-node-width);
        border-radius: var(--global-radius);
    }
</style>
