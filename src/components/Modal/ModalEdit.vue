<template>
  <form class="edit-form" @submit.prevent="submitHandler">
    <label for="edit-name">Name</label>
    <input
      class="edit-form__name"
      type="text"
      name="name"
      id="edit-name"
      v-model.trim="name"
    />
    <label for="edit-descr">Description</label>
    <textarea
      class="edit-form__descr"
      name="description"
      id="edit-descr"
      v-model.trim="description"
    ></textarea>
    <button class="btn" type="submit">Done</button>
  </form>
</template>

<script>
export default {
  name: "ModalEdit",
  data: () => ({
    name: "",
    description: "",
  }),
  props: ["beer"],
  created() {
    this.name = this.beer.name;
    this.description = this.beer.description;
  },
  methods: {
    submitHandler() {
      if (!this.name || !this.description) return;
      this.$emit("edit", this.beer.id, this.name, this.description);
    },
  },
};
</script>
