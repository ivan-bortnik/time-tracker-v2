<template>
    <div id="component-root">

        <div id="panel">
            <h2>Vraiment ?</h2>
            <p>Le temps sera définitement enregistré et vous ne pourrez plus reprendre cette session.</p>
            <p class="button" id="yes" @click="resetTimer">Yes</p>
            <p class="button" id="no" @click="resumeTimer">No</p>
        </div>  

    </div>
</template>

<script>

export default {
    name: 'TimerResetConfirmation',
    methods: {
        resetTimer () {
            this.$parent.resetTimer();
        },

        resumeTimer () {
            this.$parent.startTimer();
        } 
    }
}

</script>

<style scoped src="./TimerResetConfirmation.css"></style>