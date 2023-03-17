<template>
    <div id="component-root">

        <p class="label">En cours</p>
        <p class="task">{{ task }}</p>
        <div class="timer">
            <p>
                {{ formatTime() }}
            </p>   
        </div>

        <div class="buttons">
            <img :src="btnSrc" alt="" class="button" @click="toggleTimer">
            <img src="../../assets/stop.png" alt="" class="button" @click="askForConfirmation">
        </div>

        <timer-reset-confirmation v-if="askingForConfirmation"/>

    </div>
</template>

<script>

import TimerResetConfirmation from '../TimerResetConfirmation/TimerResetConfirmation.vue';

export default {
    name: 'TimerTab',
    components: {
        'timer-reset-confirmation': TimerResetConfirmation
    },
    props: ["task"],
    data () {
        return {

            isRunning: false,
            elapsedTime: 0,
            interval: null,
            askingForConfirmation: false,

            buttonStart: require('../../assets/start.png'),
            buttonPause: require('../../assets/pause.png'),

            btnSrc: require('../../assets/start.png')

        }
    },
    methods: {

        toggleTimer () {
            if (this.isRunning) {
                this.stopTimer();
                this.btnSrc = this.buttonStart;

            } else {
                this.startTimer();
                this.btnSrc = this.buttonPause;
            }
        },

        startTimer () {
            this.askingForConfirmation = false;
            this.isRunning = true;
            this.interval = setInterval(() => {
                this.elapsedTime++;
            }, 1000);
        },

        stopTimer () {
            this.isRunning = false;
            if (this.interval != null) {
                clearInterval(this.interval);
            }
        },

        askForConfirmation () {
            this.stopTimer();
            this.askingForConfirmation = true;
        },

        resetTimer () {
            this.askingForConfirmation = false;
            this.stopTimer();
            this.$parent.saveInHistory(this.elapsedTime);
            this.elapsedTime = 0;
            this.btnSrc = this.buttonStart;
        },

        /**
         * Returns the elapsed time in a HH:MM:SS format
         */
        formatTime () {
            let hours   = Math.floor(this.elapsedTime / 3600);
            let minutes = Math.floor((this.elapsedTime - (hours * 3600)) / 60);
            let seconds = this.elapsedTime - (hours * 3600) - (minutes * 60);

            if (hours   < 10) {hours   = "0"+hours;}
            if (minutes < 10) {minutes = "0"+minutes;}
            if (seconds < 10) {seconds = "0"+seconds;}
            return `${hours}:${minutes}:${seconds}`;
        }

    }
}

</script>

<style scoped src="./TimerTab.css"></style>