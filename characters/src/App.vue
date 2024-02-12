<template>
  <div>
    <div class="mySearchContainer">
      <div class="mySearchContainerinside">
        <img class="icoSearch" :src="iconsearch" alt="search icon" />
        <input v-model="searchQuery" type="text" placeholder="поиск" />
        <select v-model="selected" id="filter" name="status">
          <option value="alive">alive</option>
          <option value="dead">dead</option>
        </select>
        <button @click="fetchHeroSearch">Apply</button>
        <!-- changed onclick to click -->
      </div>
    </div>

    <my-card-characters :characters="characters" />
    <pagination
      :current-page="currentPage"
      :total-page="totalPage"
      @update-page="updatePage"
      :has-prev="prev !== null"
      :has-next="next !== null"
    />
  </div>
</template>

<script>
import iconsearch from "../src/icons/search-circle.svg";
import axios from "axios";
import MyCardCharacters from "./components/MyCardCharacters.vue";
import Pagination from "./components/Pagination.vue";

export default {
  components: { MyCardCharacters, Pagination },
  data() {
    return {
      characters: [],
      searchQuery: "",
      selected: "alive",
      currentPage: 1,
      totalPage: 0,
      prev: null,
      next: null,
    };
  },
  methods: {
    async fetchCharacters(url) {
      try {
        const response = await axios.get(url);
        this.characters = response.data.results;
        this.totalPage = response.data.info.pages;
        this.prev = response.data.info.prev;
        this.next = response.data.info.next;
        this.fetchError = null; // Reset fetch error
        console.log(response);
      } catch (error) {
        aler("Error", error);
        console.error("Fetch characters error:", error);
      }
    },
    async fetchHeroSearch() {
      const url = `https://rickandmortyapi.com/api/character/?name=${this.searchQuery}&status=${this.selected}`;
      this.fetchCharacters(url);
    },
    updatePage(page) {
      this.currentPage = page;
      const url = `https://rickandmortyapi.com/api/character/?page=${page}&name=${this.searchQuery}&status=${this.selected}`;
      this.fetchCharacters(url);
    },
    goToNextPage() {
      if (this.next) {
        this.fetchCharacters(this.next);
      }
    },
    goToPrevPage() {
      if (this.prev) {
        this.fetchCharacters(this.prev);
      }
    },
  },
  mounted() {
    this.fetchCharacters(
      `https://rickandmortyapi.com/api/character/?page=${this.currentPage}`
    );
  },
  computed: {
    iconsearch() {
      return iconsearch;
    },
  },
};
</script>

<style></style>
