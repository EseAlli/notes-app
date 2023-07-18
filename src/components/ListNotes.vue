<template>
  <div class="container">
    <div class="notes" v-if="notes">
      <note
        v-for="note in sortedNotes"
        :key="note.id"
        v-on:delete-note="deleteNote"
        :note="note"
        v-on:editNote="editNote"
      ></note>
    </div>
  </div>
</template>

<script>
import Note from "./Note.vue";
export default {
  props: ["notes"],
  components: {
    Note,
  },
  computed: {
    sortedNotes() {
      return this.notes.slice().sort((a, b) => a.date_updated - b.date_updated);
    },
  },
  methods: {
    deleteNote(note) {
      const noteIndex = this.notes.indexOf(note);
      this.notes.splice(noteIndex, 1);
      alert("Note deleted!");

      // Update notes in local storage
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },
    editNote(updatedNote) {
      const noteIndex = this.notes.findIndex(
        (note) => note.id === updatedNote.id
      );
      if (noteIndex !== -1) {
        this.notes.splice(noteIndex, 1, updatedNote);
        alert("Note updated!");

        // Update notes in local storage
        localStorage.setItem("notes", JSON.stringify(this.notes));
      }
    },
  },
};
</script>

<style scoped>
.notes {
  display: flex !important ;
  justify-content: space-around;
  gap: 0.75rem;
  flex-wrap: wrap;
}
@media (max-width: 600px) {
  .notes {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>
