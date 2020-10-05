<template>
  <li class="beer-list__item">
    <div class="beer-list__item-content">
      <div class="beer-list__item-head">
        <span class="beer-list__item-num">{{ index + 1 }}.</span> <span class="beer-list__item-name">{{ beer.name }}</span>
      </div>
      <p class="beer-list__item-info">
        <span class="beer-list__item-title">Description:</span> {{ beer.description }}
      </p>
      <p class="beer-list__item-info">
        <span class="beer-list__item-title">Brewers tips:</span> {{ beer.brewers_tips }}
      </p>
      <div class="beer-list__item-btns">
        <button class="btn beer-list__item-edit" @click="editHandler">
          Edit
        </button>
        <button class="btn btn-delete" @click="deleteHandler">Delete</button>
      </div>
    </div>
    <div class="beer-list__item-img">
      <img :src="beer.image_url" alt="Beer image">
    </div>
  </li>
</template>

<script>
export default {
  name: "BeerItem",
  props: ["beer", "index"],
  methods: {
    editHandler() {
      this.$emit("edit", this.beer.id);
    },
    deleteHandler() {
      this.$emit("delete", this.beer.id);
    },
  },
};
</script>