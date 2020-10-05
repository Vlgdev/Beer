<template>
  <div id="app">
    <div class="container">
      <h1 class="title">Beer list</h1>
      <ul class="beer-list" v-if="beerList.length">
        <BeerItem
          v-for="(beer, i) of beerList"
          :key="beer.id"
          :beer="beer"
          :index="i"
          @edit="openEditModal"
          @delete="deleteBeer"
        />
      </ul>
      <Loader v-if="loading && beerPage === 1" />
      <div class="load-more" v-else-if="!noBeerToLoad">
        <button
          class="btn btn-black load-more__btn"
          :disabled="loading"
          @click="loadBeer"
        >
          {{ loading ? "Loading" : "Show next" }}
        </button>
      </div>
    </div>
    <Modal
      v-if="modalSettings"
      :settings="modalSettings"
      @close="closeModal"
      @edit="editBeer"
    />
  </div>
</template>

<script>
import Loader from "./components/Loader";
import BeerItem from "./components/BeerItem";
import Modal from "./components/Modal";

export default {
  name: "App",
  components: {
    Loader,
    BeerItem,
    Modal,
  },
  data: () => ({
    loading: true,
    beerList: [],
    noBeerToLoad: false,
    beerPage: 1,
    modalSettings: null,
  }),
  async mounted() {
    this.loadBeer();
  },
  methods: {
    async loadBeer() {
      console.log("loading");
      this.loading = true;

      const response = await fetch(
        `https://api.punkapi.com/v2/beers?page=${this.beerPage}&limit=25`
      );
      const data = await response.json();

      this.beerPage++;

      if (data && data.length) {
        this.beerList.push(...data);
      } else {
        this.noBeerToLoad = true;
      }

      this.loading = false;
    },
    editBeer(id, name, description) {
      this.beerList = this.beerList.map((b) => {
        if (b.id === id) {
          b.name = name;
          b.description = description;
        }

        return b;
      });
      this.closeModal();
    },
    deleteBeer(id) {
      this.beerList = this.beerList.filter((b) => b.id !== id);
    },
    openEditModal(id) {
      this.modalSettings = {
        subject: "editBeer",
        beer: this.beerList.find((b) => b.id === id),
      };
    },
    closeModal() {
      this.modalSettings = null;
    },
  },
};
</script>

<style lang="scss">
@import "~normalize.css";
@import "./assets/scss/style.scss";
</style>
