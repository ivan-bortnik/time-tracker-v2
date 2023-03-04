<template>
    <div id="component-root">

        <img src="../../assets/timer.png" @click="switchTab(0)">
        <img src="../../assets/timer.png" @click="switchTab(1)">
        <img src="../../assets/timer.png" @click="switchTab(2)">

    </div>
</template>

<script lang="ts">

export default {
    name: 'Navbar',
    methods: {

        switchTab (tabIdx) {
             this.$parent.switchTab(tabIdx);
        }

    }
}

</script>

<style scoped>

#component-root {
    background-color: #222f3e;
    text-align: center;
    position: absolute;
    bottom: 0;
    width: 100vw;
    height: 64px;
}

img {
    width: 40px;
    padding: 6px 32px;
}

</style>