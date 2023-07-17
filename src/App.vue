<template>
  <div class="container">
    <h1 class="header">Notes App</h1>
    <div class="flex justify-end">
      <button id="show-modal" @click="showModal = true">+ Add Note</button>
    </div>
    <create-note
      v-on:create-note="createNote"
      :show="showModal"
      @close="showModal = false"
      :edit="false"
    ></create-note>
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
    CreateNote,
  },
  data() {
    return {
      showModal: false,
      notes: [],
    };
  },
  methods: {
    createNote(note) {
      this.notes.push(note);
      alert("Note created!");

      // Save notes to local storage
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },
    fetchNotes() {
      // Fetch notes from local storage
      const savedNotes = localStorage.getItem("notes");
      if (savedNotes) {
        this.notes = JSON.parse(savedNotes);
      }
    },
  },
  created() {
    // Fetch notes when the component is created
    this.fetchNotes();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 20px;
}

button {
  border: none;
  background: transparent;
}

button:hover {
  cursor: pointer;
}

.container {
  max-width: 90%;
  margin: 0 auto;
  padding: 8px 0;
}

.header {
  color: #6fa8dc;
}

.flex {
  display: flex;
}

.justify-end {
  justify-content: end;
}

.gap-2 {
  gap: 0.5rem;
}

.flex-col {
  flex-direction: column;
}

.items-end {
  align-items: flex-end;
}
</style>
