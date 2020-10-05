<template>
  <div class="modal" @click="closeHandler">
    <div class="modal__content" @click.stop>
      <ModalEdit
        v-if="settings.subject === 'editBeer'"
        :beer="settings.beer"
        @edit="editHandler"
      />
      <div class="close modal__close" @click="closeHandler"></div>
    </div>
  </div>
</template>

<script>
import ModalEdit from "./Modal/ModalEdit";

export default {
  name: "Modal",
  props: ["settings"],
  components: {
    ModalEdit,
  },
  methods: {
    editHandler(id, name, description) {
      this.$emit("edit", id, name, description);
    },
    closeHandler() {
      console.log(event);
      this.$emit('close')
    }
  },
};
</script>