<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    totalPages: {
      type: Number,
      required: true,
    },
    itemsPerPage: {
      type: Number,
      default: 2,
    },
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
    },
  },
  methods: {
    prevPage() {
      if (this.currentPage > 1) {
        this.$emit("update:currentPage", this.currentPage - 1);
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit("update:currentPage", this.currentPage + 1);
      }
    },
    onPageClick(page) {
      this.$emit("update:currentPage", page);
    },
  },
};
</script>

<template>
  <div class="pagination">
    <button @click="prevPage" class="prv_nxt prv" :disabled="isInFirstPage">
      ≼
    </button>
    <span v-for="page in pages" :key="page">
      <button
        class="pag_num"
        :class="{ active: currentPage === page }"
        @click="onPageClick(page)"
      >
        {{ page }}
      </button>
    </span>

    <button @click="nextPage" class="prv_nxt nxt" :disabled="isInLastPage">
      ≽
    </button>
  </div>
</template>

<style scoped>
.prv_nxt {
  border: 3px solid #ffffff;
  font-size: 1em;
  background-color: #ae4a4a;
  color: white;
  padding: 2px 10px;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.5s;
}

.prv,
.nxt{
  margin: 0 20px;
}

.prv_nxt:hover {
  background-color: white;
  color: #ae4a4a;
  border: 3px solid transparent;
}
.pagination {
  margin-top: 3%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.pag_num {
  margin: 0 5px;
  font-size: 1.1em;
  background-color: #ae4a4a;
  background: #ae4a4a;
  padding: 0 10px;
  cursor: pointer;
  border: solid #ffffff;
  transition: all 0.5s;
  border-radius: 20px;
}
.pag_num:hover{
  background-color: black;
  color: white;
}
button {
  margin: 0 5px;
}

.active {
  background-color: #ffffff;
  color: #000000;
}
</style>
