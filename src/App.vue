<template>
  <div id="app">
    <NavBar class="nav-bar"></NavBar>
    <div class="main-content">
      <SideMenu class="side-menu"></SideMenu>
      <MailView class="mail-view"></MailView>
    </div>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import SideMenu from './components/SideMenu.vue'
import MailView from './components/MailView.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    SideMenu,
    MailView
  }
}
</script>

<style>
body {
  margin: 0;
  overflow: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  height: 100vh;
  margin: 0;
}

.nav-bar {
  width: 100%;
}

.main-content {
  display: flex;
  flex: 1;
  overflow: hidden;
}

.side-menu {
  transition: width 0.3s;
}

.mail-view {
  flex: 1;
  padding: 20px;
  transition: margin-left 0.3s;
  overflow: hidden; 
}
</style>
