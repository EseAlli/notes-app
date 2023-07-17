<template>
  <div class="note">
    <!-- <p>{{ note.title }}</p> -->
    <p class="title">Lunch at 12PM</p>
    <p>Milk, Coffee, cookies</p>
    <p>17/07/2023</p>
    <div class="flex gap-2">
      <p class="edit-btn" @click="showModal = true">Edit</p>
      <p class="delete-btn" @click="showDeleteModal = true">Delete</p>
    </div>
    <edit-note
      :show="showModal"
      @close="showModal = false"
      :note="note"
    ></edit-note>
    <Teleport to="body">
      <modal :show="showDeleteModal" @close="showDeleteModal = false">
        <template #header>
          <h3>Delete Note</h3>
        </template>
        <template #body>
          <div>
            <button>Yes</button>
            <button @click="showDeleteModal = false">No</button>
          </div>
        </template>
      </modal>
    </Teleport>
  </div>
</template>

<script>
import EditNote from "./NoteForm";
import Modal from "./Modal";
export default {
  name: "Note",
  props: ["note"],
  components: {
    EditNote,
    Modal,
  },
  data() {
    return {
      showModal: false,
      showDeleteModal: false,
    };
  },
};
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

.title:hover {
  color: #6fa8dc;
  cursor: pointer;
}

.title {
  font-weight: 600;
}

.edit-btn:hover,
.delete-btn:hover {
  cursor: pointer;
}

@media (max-width: 768px) {
  .note {
    width: auto;
    margin: 0.5rem 0;
  }
}
</style>
