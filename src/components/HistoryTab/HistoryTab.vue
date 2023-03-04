<template>
    <div id="component-root">

        <h2>History</h2>

        <p v-for="(item, idx) in history" :key="idx">{{ item.name }} | {{ item.time }} | {{ item.date }}</p>

    </div>
</template>

<script lang="ts">

export default {
    name: 'History',
    props: ["history"]
}

</script>

<style scoped>

#component-root {
    width: 100vw;
}

</style>