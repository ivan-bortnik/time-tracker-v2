<template>
    <div id="component-root">

        <div id="panel">
            <h2>Nouveau Projet</h2>

            <p>Nom</p>
            <input type="text" name="" id="" v-model="pName">

            <br>

            <p>Client</p>
            <input type="text" name="" id="" v-model="pClient">
            
            <br>
            <button @click="create()">CREER</button>

        </div>  

    </div>
</template>

<script>

export default {
    name: 'NewProject',
    data () {
        return {
            pName: '',
            pClient: ''
        }
    },
    methods: {
        create () {
            this.$parent.$parent.projects.unshift({
                name: this.pName,
                time: 0
            });
            this.$parent.isNewProjectWindowVisible = false;
            this.$parent.$parent.save();
        }
    }
}

</script>

<style scoped src="./NewProject.css"></style>