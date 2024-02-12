<template>
  <div class="pagination">
    <button @click="previousPage" :disabled="currentPage === 1 || !hasPrev">
      Previous
    </button>
    <span>Page {{ currentPage }} of {{ totalPage }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPage || !hasNext">
      Next
    </button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    totalPage: {
      type: Number,
      required: true,
    },
    hasPrev: {
      type: Boolean,
      required: true,
    },
    hasNext: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    previousPage() {
      this.$emit("update-page", this.currentPage - 1);
    },
    nextPage() {
      this.$emit("update-page", this.currentPage + 1);
    },
  },
};
</script>

<style>
.pagination {
  margin-top: 20px;
  text-align: center;
}
.pagination button {
  margin: 0 5px;
}
</style>
