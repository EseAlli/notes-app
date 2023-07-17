<template>
  <div class="note">
    <!-- <p>{{ note.title }}</p> -->
    <p class="title">Lunch at 12PM</p>
    <p>Milk, Coffee, cookies</p>
    <p>17/07/2023</p>
  </div>
</template>

<script>
export default {
  name: "Note",
  props: ["note"],
};
console.log();
</script>

<style scoped>
.note {
  border: 1px solid #6fa8dc;
  border-radius: 8px;
  margin: 1rem 0;
  width: 100%;
  padding: 0.75rem;
  text-align: left;
}

.note:hover {
  background: #6fa8dc;
  cursor: pointer;
}

.title {
  font-weight: 600;
}
@media (max-width: 768px) {
  .note {
    width: auto;
    margin: 0.5rem 0;
  }
}
</style>
