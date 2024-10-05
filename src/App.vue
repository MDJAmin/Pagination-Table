<template>
  <div>
    <TableView :items="items"/>
  </div>
</template>

<script>
import TableView from "@/view/TableView.vue";

export default {
  // registering
  components: {TableView},
  data() {
    return {
      items: []
    };
  },
  // lifecycle hooks
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => {
          this.items = data;
        })
        .catch(error => {
          console.error(error);
        });
  }
};
</script>