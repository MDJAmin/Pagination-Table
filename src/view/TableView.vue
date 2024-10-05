<template>
  <div>
    <VTable :items="paginatedItems" />
    <VPagination
        :totalPages="totalPages"
        :currentPage="currentPage"
        :itemsPerPage="itemsPerPage"
        @update:currentPage="updateCurrentPage"
    />
  </div>
</template>

<script>
import {computed, ref} from "vue";
import VTable from "@/components/VTable.vue";
import VPagination from "@/components/VPagination.vue";

export default {
  components: {VPagination, VTable},
  props: {
    items: {
      type: Array,
      required: true
    },
    itemsPerPage: {
      type: Number,
      default: 2
    }
  },
  setup(props) {
    const currentPage = ref(1);

    const totalPages = computed(() => Math.ceil(props.items.length / props.itemsPerPage));

    const paginatedItems = computed(() => {
      const start = (currentPage.value - 1) * props.itemsPerPage;
      const end = start + props.itemsPerPage;
      return props.items.slice(start, end);
    });
    const updateCurrentPage = (newPage) => {
      currentPage.value = newPage;
    };
    return {
      currentPage,
      totalPages,
      paginatedItems,
      updateCurrentPage,
    };
  },
}

</script>
