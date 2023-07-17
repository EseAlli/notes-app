<template>
  <div id="app">
    <h1 class="header">Notes App</h1>
    <list-notes v-bind:notes="notes"></list-notes>
  </div>
</template>

<script>
import ListNotes from "./components/ListNotes.vue";

export default {
  name: "App",
  components: {
    ListNotes,
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
  margin-top: 60px;
}

.header {
  color: #6fa8dc;
}
</style>
