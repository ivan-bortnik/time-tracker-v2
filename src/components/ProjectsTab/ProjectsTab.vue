<template>
    <div id="component-root">

        <new-project v-if="isNewProjectWindowVisible"/>

        <h2>Projets</h2>

        <div class="container">
            <p v-for="(item, idx) in projects" :key="idx" @click="setProject(idx)"
            :class="($parent.currentProject == idx) ? 'current' : ''">
                <span class="name">{{ item.name }}</span><br>
                <span class="time">{{ formatTime(item.time) }}</span>
            </p>
        </div>

        <p class="add-project" @click="isNewProjectWindowVisible = true">Ajouter un projet</p>

    </div>
</template>

<script>

import NewProject from '../NewProject/NewProject.vue'

export default {
    name: 'ProjectsTab',
    components: {
         'new-project': NewProject
    },
    props: ['projects'],
    data () {
        return {
            isNewProjectWindowVisible: false
        }
    },
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
        },

        setProject (idx) {
            this.$parent.currentProject = idx;
        }
    }
}

</script>

<style scoped src="./ProjectsTab.css"></style>