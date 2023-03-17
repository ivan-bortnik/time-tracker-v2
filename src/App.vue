<template>
  <div id="app">

    <div id="tabs" :style="{ left: -selectedTab * 100 + 'vw' }">
      <projects-tab/>
      <timer-tab :task="projects[currentProject].name"/>
      <history-tab :history="history"/>
    </div>

    <navbar/>

  </div>
</template>

<script>
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
  data () {
    return {
      selectedTab: 1,
      currentProject: 0,
      projects: [
        {
          name: "Test Project 1",
          time: 541
        }
      ],
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