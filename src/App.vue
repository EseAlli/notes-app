<template>
  <div id="app">
    <h1 class="header">Notes App</h1>
    <NoteItem />
  </div>
</template>

<script>
import NoteItem from "./components/Note.vue";

export default {
  name: "App",
  components: {
    NoteItem,
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
