<template>
  <div class="container">
    <h1 class="header">Notes App</h1>
    <div class="flex justify-end">
      <button id="show-modal" @click="showModal = true">+ Add Note</button>
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
    CreateNote,
  },
  data() {
    return {
      showModal: false,
      notes: [
        {
          id: 1,
          title: "Lunch at 12PM",
          description: "Call Robert to remember him.",
        },
        {
          id: 2,
          title: "Gym with Jane",
          description: "She is needing your motivation...",
        },
        {
          id: 3,
          title: "Call mom",
          description: "Ask her about the cats?",
        },
        {
          id: 4,
          title: "Call mom",
          description: "Ask her about the cats?",
        },
      ],
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
</style>
