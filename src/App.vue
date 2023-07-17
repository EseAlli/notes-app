<template>
  <div class="container">
    <h1 class="header">Notes App</h1>
    <div>
      <button id="show-modal" @click="showModal = true">Add Note</button>
    </div>
    <create-note :show="showModal" @close="showModal = false"></create-note>
    <list-notes v-bind:notes="notes"></list-notes>
  </div>
</template>

<script>
import ListNotes from "./components/ListNotes.vue";
import CreateNote from "./components/NoteForm";

export default {
  name: "App",
  components: {
    ListNotes,
    // Modal,
    CreateNote,
  },
  data() {
    return {
      showModal: false,
    };
  },
};
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 20px;
}
.container {
  max-width: 90%;
  margin: 0 auto;
  padding: 8px 0;
}

.header {
  color: #6fa8dc;
}
</style>
