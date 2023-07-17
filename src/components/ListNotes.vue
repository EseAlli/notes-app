<template>
  <div class="container">
    <div class="notes">
      <note
        v-for="note in sortedNotes"
        :key="note.id"
        v-on:delete-note="deleteNote"
        :note="note"
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
