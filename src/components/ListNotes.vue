<template>
  <div class="container">
    <div class="notes">
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
      console.log(note, "note to delete");
    },
    editNote(updatedNote) {
      console.log("updated", updatedNote.id, this.notes);
      const noteIndex = this.notes.findIndex(
        (note) => note.id === updatedNote.id
      );
      if (noteIndex !== -1) {
        this.notes.splice(noteIndex, 1, updatedNote);
        alert("Note updated!");
      }
    },
    console(notes) {
      console.log(notes);
    },
  },
};
</script>

<style scoped>
.notes {
  display: flex !important ;
  justify-content: space-between;
  gap: 1rem;
  /* flex-wrap: wrap; */
}
@media (max-width: 768px) {
  .notes {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>
