<template>
    <div id="component-root">

        <h2>Historique</h2>

        <div class="container">
            <p v-for="(item, idx) in history" :key="idx">
                <span class="name">{{ item.name }}</span><br>
                <span class="date">{{ item.date }}</span>
                <span class="time">{{ formatTime(item.time) }}</span>
            </p>
        </div>

    </div>
</template>

<script>

export default {
    name: 'History',
    props: ["history"],
    methods: {
    /**
     * Returns the elapsed time in a HH:MM:SS format
     */
    formatTime (time) {
        let hours   = Math.floor(time / 3600);
        let minutes = Math.floor((time - (hours * 3600)) / 60);
        let seconds = time - (hours * 3600) - (minutes * 60);

        if (hours   < 10) {hours   = "0"+hours;}
        if (minutes < 10) {minutes = "0"+minutes;}
        if (seconds < 10) {seconds = "0"+seconds;}
        return `${hours}:${minutes}:${seconds}`;
    }
}
}

</script>

<style scoped src="./HistoryTab.css"></style>