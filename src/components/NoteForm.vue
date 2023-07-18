<template>
  <div v-if="show">
    <modal :show="isShown" @close="hideModal">
      <template #header>
        <h3>Note</h3>
      </template>
      <template #body>
        <form>
          <input
            placeholder="Title"
            :value="edit ? note.title : title"
            @input="
              edit
                ? (note.title = $event.target.value)
                : (title = $event.target.value)
            "
            required
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
            required
          ></textarea>

          <p class="characters">
            {{ (edit ? note.description : description).length }}
            Characters
          </p>
          <button v-on:click="submitNote()">Submit</button>
        </form>
      </template>
    </modal>
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
      isShown: false,
      title: "",
      description: "",
    };
  },
  mounted() {
    this.isShown = this.show;
  },
  watch: {
    show(newVal) {
      this.isShown = newVal;
    },
  },
  methods: {
    hideModal() {
      this.isShown = false;
      this.$emit("close");
    },
    createNote() {
      if (this.title !== "" || this.description !== "") {
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
      } else {
        alert("Please enter a note - Missing title or Description");
      }
    },
    editNote() {
      this.$emit("edit-note", {
        id: this.note.id,
        title: this.note.title,
        description: this.note.description,
        date_created: this.note.date_created,
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
