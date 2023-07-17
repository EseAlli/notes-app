<template>
  <div v-if="show">
    <Teleport to="body">
      <modal :show="show" @close="show = false">
        <template #header>
          <h3>Note</h3>
        </template>
        <template #body>
          <div>
            <input
              placeholder="Title"
              :value="edit ? note.title : title"
              @input="
                edit
                  ? (note.title = $event.target.value)
                  : (title = $event.target.value)
              "
            />
            <textarea
              rows="10"
              placeholder="Start typing"
              :value="edit ? note.description : description"
              @input="
                edit
                  ? (note.description = $event.target.value)
                  : (description = $event.target.value)
              "
            ></textarea>

            <p class="characters">Characters</p>
            <button v-on:click="submitNote()">Submit</button>
          </div>
        </template>
      </modal>
    </Teleport>
  </div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  props: {
    show: Boolean,
    note: {},
    edit: Boolean,
  },
  components: {
    Modal,
  },
  data() {
    return {
      showModal: false,
      title: "",
      description: "",
    };
  },
  methods: {
    createNote() {
      this.$emit("create-note", {
        id: Math.random() * 100,
        title: this.title,
        description: this.description,
        date_created: new Date(),
        date_updated: new Date(),
      });
      this.title = "";
      this.description = "";
      this.$emit("close");
    },
    editNote() {
      this.$emit("edit-note", {
        id: this.note.id,
        title: this.note.title,
        description: this.note.description,
        date_updated: new Date(),
      });
      this.$emit("close");
    },
    submitNote() {
      this.edit ? this.editNote() : this.createNote();
    },
  },
};
</script>

<style scoped>
input,
textarea {
  border: none !important;
  margin: 0.5rem 0;
  padding: 0.75rem 0;
  width: 100%;
}

input:focus,
textarea:focus {
  outline: none;
}

.characters {
  text-align: right;
  font-size: 0.75rem;
  color: grey;
}
</style>
