<template>
  <div id="app">
    <Header />
    <Navbar />
    <div class="view-container">
      <router-view />
    </div>
  </div>
</template>

<script lang="js">
import Header from "./components/Header.vue"
import Navbar from "./components/Navbar.vue"


export default {
  name: 'App',
  data() {
    return {
      headerTitle: "Usuários",
    }
  },
  components: {
    Header,
    Navbar,
},
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

.click {
  cursor: pointer;
}

.disabled {
  cursor: no-drop;
}
</style>
