<template>
  <div id="app">

    <div id="tabs" :style="{ left: -selectedTab * 100 + 'vw' }">
      <projects-tab :projects="projects"/>
      <timer-tab :task="projects.length > 0 ? projects[currentProject].name : 'rien'"/>
      <history-tab :history="history"/>
    </div>

    <navbar/>

  </div>
</template>

<script>

//const electron = require('electron')
const settings = require('electron-settings');

import Navbar from './components/Navbar/Navbar.vue';
import TimerTab from './components/TimerTab/TimerTab.vue';
import HistoryTab from './components/HistoryTab/HistoryTab.vue';
import ProjectsTab from './components/ProjectsTab/ProjectsTab.vue';
export default {
  name: 'App',
  components: {
    'navbar': Navbar,
    'timer-tab': TimerTab,
    'history-tab': HistoryTab,
    'projects-tab': ProjectsTab
  },
  beforeMount() {
    this.load();
  },
  data () {
    return {
      selectedTab: 1,
      currentProject: 0,
      projects: [],
      history: []
      
    }
  },
  methods: {
    switchTab (tabIdx) {
      this.selectedTab = tabIdx
    },
    saveInHistory (time) {
      let today = new Date().toLocaleDateString();
      this.history.unshift(
        {
          name: this.projects[this.currentProject].name,
          time: time,
          date: today
        }
      );

      this.projects[this.currentProject].time += time;
      this.save();
    },
    async save() {
      await settings.set('projects', this.projects);
      await settings.set('history', this.history);
    },
    async load() {
      settings.get('history').then(val => {
        if (typeof val !== 'undefined') { this.history = val; }
      });
      settings.get('projects').then(val => {
          if (typeof val !== 'undefined') { this.projects = val; }
      });
    }
  }
}
</script>

<style>
#app {
  font-family: Poppins;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  background-color: #222f3e;
}
#tabs {
  position: absolute;
  width: 300vw;
  height: calc(100vh - 64px);
  display: flex;
  flex-direction: row;
  transition: .15s;
}
h2 {
  padding: 0 16px;
}
</style>