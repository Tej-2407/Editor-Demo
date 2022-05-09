<template>
  <div id="app">
    <b-navbar toggleable="lg" type="dark" variant="dark">
          <b-nav-item v-b-toggle.sidebar-backdrop><b-icon icon="box-arrow-left"></b-icon></b-nav-item>
     
      <b-navbar-brand><router-link to="/">Editor</router-link></b-navbar-brand>
      <b-navbar-toggle target="navbar-toggle-collapse"></b-navbar-toggle>

      <b-collapse id="navbar-toggle-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item><router-link to="/demo1">Demo 1</router-link></b-nav-item>
          <b-nav-item><router-link to="/demo2">Demo 2</router-link></b-nav-item>
          <b-nav-item><router-link to="/demo3">Demo 3</router-link></b-nav-item>
          <!-- <b-nav-item><router-link to="/demo4">Demo 4</router-link></b-nav-item> -->
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <b-sidebar
      id="sidebar-backdrop"
      title="Sidebar"
      :backdrop-variant="variant"
      backdrop
      shadow
    >
       <div class="px-3 py-2">
        <b-img src="https://picsum.photos/500/500/?image=54" fluid thumbnail></b-img>
      </div>
    </b-sidebar>
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      variant: 'dark'
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow-x: hidden;
  background-color: aliceblue;
  height: 100vh;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  float: left;
  display: block;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
