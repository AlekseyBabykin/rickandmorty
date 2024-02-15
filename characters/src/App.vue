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
import { ref, reactive, onMounted } from "vue";
import iconsearch from "../src/icons/search-circle.svg";
import axios from "axios";
import MyCardCharacters from "./components/MyCardCharacters.vue";
import Pagination from "./components/Pagination.vue";

export default {
  components: { MyCardCharacters, Pagination },
  setup() {
    const characters = ref([]);
    const searchQuery = ref("");
    const selected = ref("alive");
    const currentPage = ref(1);
    const totalPage = ref(0);
    const prev = ref(null);
    const next = ref(null);

    const fetchCharacters = async (url) => {
      try {
        const response = await axios.get(url);
        characters.value = response.data.results;
        totalPage.value = response.data.info.pages;
        prev.value = response.data.info.prev;
        next.value = response.data.info.next;
        console.log(response);
      } catch (error) {
        alert("Error");
        console.error("Fetch characters error:", error);
      }
    };

    const fetchHeroSearch = () => {
      const url = `https://rickandmortyapi.com/api/character/?name=${searchQuery.value}&status=${selected.value}`;
      fetchCharacters(url);
    };

    const updatePage = (page) => {
      currentPage.value = page;
      const url = `https://rickandmortyapi.com/api/character/?page=${page}&name=${searchQuery.value}&status=${selected.value}`;
      fetchCharacters(url);
    };

    const goToNextPage = () => {
      if (next.value) {
        fetchCharacters(next.value);
      }
    };

    const goToPrevPage = () => {
      if (prev.value) {
        fetchCharacters(prev.value);
      }
    };

    onMounted(() => {
      fetchCharacters(
        `https://rickandmortyapi.com/api/character/?page=${currentPage.value}`
      );
    });

    return {
      iconsearch,
      characters,
      searchQuery,
      selected,
      currentPage,
      totalPage,
      prev,
      next,
      fetchHeroSearch,
      updatePage,
      goToNextPage,
      goToPrevPage,
    };
  },
};
</script>

<style></style>
