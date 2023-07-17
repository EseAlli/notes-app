<template>
  <div class="container">
    <div class="notes">
      <note v-for="note in notes" v-bind:key="note.id"></note>
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
};
</script>

<style scoped>
.container {
  max-width: 90%;
  margin: 0 auto;
  padding: 8px 0;
}
.notes {
  display: flex !important ;
  justify-content: space-between;
  gap: 1rem;
}
@media (max-width: 768px) {
  .notes {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>
