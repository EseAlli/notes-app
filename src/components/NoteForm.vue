<template>
  <div v-if="show">
    <Teleport to="body">
      <modal :show="show" @close="show = false">
        <template #header>
          <h3>Note</h3>
        </template>
        <template #body>
          <div>
            <input placeholder="Title" v-model="title" />
            <textarea
              name=""
              id=""
              rows="10"
              placeholder="Start typing"
              v-model="description"
            ></textarea>
            <p class="characters">Characters</p>
            <button @click="createNote">Submit</button>
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
      console.log(this.title);
      this.$emit("create-note", {
        title: this.title,
        description: this.description,
        date_created: new Date(),
        date_updated: new Date(),
      });
      this.title = "";
      this.description = "";
      this.$emit("close");
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
