<template>
  <div v-if="show">
    <Teleport to="body">
      <modal :show="show" @close="showModal = false">
        <template #header>
          <h3>Note</h3>
        </template>
        <template #body>
          <div>
            <input placeholder="Title" />
            <textarea name="" id="" cols="30" rows="10"></textarea>
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
