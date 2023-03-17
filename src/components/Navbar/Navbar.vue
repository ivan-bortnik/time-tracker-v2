<template>
    <div id="component-root">

        <div class="area">
            <img src="../../assets/projects.png" @click="switchTab(0)">
        </div>

        <div class="area">
            <img src="../../assets/timer.png" @click="switchTab(1)">
        </div>
        
        <div class="area">
            <img src="../../assets/history.png" @click="switchTab(2)">
        </div>

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
    background-color: #192531;
    text-align: center;
    position: absolute;
    bottom: 0;
    width: 100vw;
    height: 52px;
}

.area {
    width: 50px;
    display: inline;
}

img {
    height: 40px;
    padding: 6px 32px;
    transition: .15s;
}

.area:hover > img {
    transform: translateY(-50%) scale(1.5);
    transition: .15s;
}

</style>