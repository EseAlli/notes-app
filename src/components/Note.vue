<template>
  <div class="note">
    <p class="title" @click="isContentShown = true">{{ note.title }}</p>
    <p>{{ truncate(note.description) }}</p>
    <div class="flex justify-end flex-col items-end note-footer">
      <p class="date">{{ formatDate(note.date_updated) }}</p>
      <div class="flex gap-2">
        <PencilIcon class="action-btn" @click="isShown = true" />
        <TrashIcon class="action-btn" @click="isDeleteModalShown = true" />
      </div>
    </div>

    <edit-note
      :show="isShown"
      @close="isShown = false"
      :note="note"
      :edit="true"
      v-on:edit-note="edit"
    ></edit-note>

    <modal :show="isDeleteModalShown" @close="isDeleteModalShown = false">
      <template #header>
        <h3>Delete Note</h3>
      </template>
      <template #body>
        <div>
          <button v-on:click="deleteNote(note.id)">Yes</button>
          <button @click="isDeleteModalShown = false">No</button>
        </div>
      </template>
    </modal>

    <modal :show="isContentShown" @close="isContentShown = false">
      <template #header>
        <h3>{{ note.title }}</h3>
      </template>
      <template #body>
        <div class="description">
          {{ note.description }}
        </div>
      </template>
    </modal>
  </div>
</template>

<script>
import EditNote from "./NoteForm";
import Modal from "./Modal";
import { PencilIcon } from "@vue-hero-icons/outline";
import { TrashIcon } from "@vue-hero-icons/outline";
export default {
  name: "Note",
  props: {
    note: {
      type: Object,
    },
  },
  components: {
    EditNote,
    Modal,
    PencilIcon,
    TrashIcon,
  },
  data() {
    return {
      isShown: false,
      isDeleteModalShown: false,
      isContentShown: false,
    };
  },
  watch: {
    show(newVal) {
      this.isShown = newVal;
    },
    showDeleteModal(newVal) {
      this.isDeleteModalShown = newVal;
    },
    showContentModal(newVal) {
      this.isContentModalShown = newVal;
    },
  },
  mounted() {
    this.isShown = this.show;
    this.isDeleteModalShown = this.showDeleteModal;
    this.isContentShown = this.showContentModal;
  },
  methods: {
    deleteNote(note) {
      this.$emit("delete-note", note);
      this.$emit("close");
    },
    formatDate(date) {
      var d = new Date(date),
        month = "" + (d.getMonth() + 1),
        day = "" + d.getDate(),
        year = d.getFullYear();

      if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day;

      return [year, month, day].join("-");
    },
    truncate(input) {
      return input.length > 5 ? `${input.substring(0, 30)}...` : input;
    },
    edit(note) {
      this.$emit("editNote", note);
    },
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
  max-width: 250px;
}

.note > p {
  margin: 0.25rem 0;
}

.note-footer {
  margin-top: 0.675rem;
}

.date {
  color: gray;
  font-size: 0.75rem;
}

.title:hover {
  color: #6fa8dc;
  cursor: pointer;
}

.title {
  font-weight: 600;
}

.action-btn {
  width: 16px;
}

.action-btn:hover {
  cursor: pointer;
}

.description {
  word-break: break-all;
}

@media (max-width: 600px) {
  .note {
    max-width: 100%;
    margin: 0.5rem 0;
  }
}
</style>
