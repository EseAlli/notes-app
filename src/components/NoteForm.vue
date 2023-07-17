<template>
  <div v-if="show">
    <Teleport to="body">
      <modal :show="show" @close="show = false">
        <template #header>
          <h3>Note</h3>
        </template>
        <template #body>
          <div>
            <input placeholder="Title" />
            <textarea
              name=""
              id=""
              cols="40"
              rows="10"
              placeholder="Start typing"
            ></textarea>
            <p class="characters">0 Characters</p>
            <button>Submit</button>
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
    };
  },
};
</script>

<style scoped>
input,
textarea {
  border: none !important;
  margin: 0.5rem 0;
  padding: 0.75rem 0;
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
