<script>
import {computed} from "vue";

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
  setup(props, {emit}) {
    const pages = computed(() => {
      const range = [];
      for (let i = 1; i <= props.totalPages; i++) {
        range.push(i);
      }
      return range;
    });

    // booleans
    const isInFirstPage = computed(() => props.currentPage === 1);
    const isInLastPage = computed(() => props.currentPage === props.totalPages);


    const prevPage = () => {
      if (props.currentPage > 1) {
        emit("update:currentPage", props.currentPage - 1);
      }
    };

    const nextPage = () => {
      if (props.currentPage < props.totalPages) {
        emit("update:currentPage", props.currentPage + 1)
      }
    };

    const onPageClick = (page) => {
      emit("update:currentPage", page);
    };

    return {
      pages,
      isInFirstPage,
      isInLastPage,
      prevPage,
      nextPage,
      onPageClick,
    };
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
.nxt {
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
  margin-top: 15px;
  border: 3px solid white;
}

.pag_num:hover {
  background-color: rgb(255, 255, 255);
  border: 3px solid #ae4a4a;
  color: #ae4a4a;
}

button {
  margin: 0 5px;
}

.active {
  background-color: #ffffff;
  color: #000000;
}
</style>
