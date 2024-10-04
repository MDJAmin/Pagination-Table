
<template>
  <div>
<VTable :items="paginatedItems"/>
    <VPagination :totalPages="totalPages" :currentPage="currentPage" :itemsPerPage="itemsPerPage" @update:currentPage="updateCurrentPage"/>
  </div>
</template>

<script >
import VTable from "@/components/VTable.vue";
import VPagination from "@/components/VPagination.vue";

export default {
  components: {VPagination, VTable},
  props:{
    items:{
      type:Array,
      required:true
    },
    itemsPerPage: {
      type: Number,
      default: 10
    }
  },
  data() {
    return {
      currentPage: 1
    };
  },
  computed:{
    totalPages(){
      return Math.ceil(this.items.length / this.itemsPerPage);
    },
    paginatedItems(){
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.items.slice(start, end)
    }
  },
  methods: {
    updateCurrentPage(newPage) {
      this.currentPage = newPage;
    }
  }
}

</script>
