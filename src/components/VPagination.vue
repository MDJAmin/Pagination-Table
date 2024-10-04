<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    totalPages: {
      type: Number,
      required: true
    },
    itemsPerPage: {
      type: Number,
      default: 2
    }
  },
  computed: {
    pages() {
      const range = [];
      for (let i = 1; i <= this.totalPages; i++) {
        range.push(i);
      }
      return range;
    },
    isInFirstPage() {
      return this.currentPage === 1;
    },
    isInLastPage() {
      return this.currentPage === this.totalPages;
    }
  },
  methods: {
    prevPage() {
      if (this.currentPage > 1) {
        this.$emit('update:currentPage', this.currentPage - 1);
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('update:currentPage', this.currentPage + 1);
      }
    },
    onPageClick(page) {
      this.$emit('update:currentPage', page);
    }
  }
};
</script>

<template>
  <div class="pagination">
    <button @click="prevPage" :disabled="isInFirstPage">Prv</button>
    <span v-for="page in pages" :key="page">
      <button
        :class="{ active: currentPage === page }"
        @click="onPageClick(page)"
      >
        {{ page }}
      </button>
    </span>
    
    <button @click="nextPage" :disabled="isInLastPage">Nxt</button>
  </div>
</template>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  margin: 0 5px;
}

</style>
