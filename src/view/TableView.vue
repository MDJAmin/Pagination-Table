
<template>
  <div>
<VTable :items="paginatedItems"/>
  </div>
</template>

<script >
import VTable from "@/components/VTable.vue";
import VPagination from "@/components/VPagination.vue";

export default {
  components: {VTable},
  props:{
    items:{
      type:Array,
      required:true
    },
    itemsPerPage: {
      type: Number,
      default: 2
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
      return this.items.slice((start, end))
    }
  },
}

</script>

<style scoped>

</style>