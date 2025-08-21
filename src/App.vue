<template>
  <div>
    <TableView :items="items" />
  </div>
  <div class="MDJAminDiv">
    <a
      class="MDJAmin"
      href="https://github.com/MDJAmin"
      target="_blank"
      >MDJAmin</a
    >
  </div>
</template>

<script>
import TableView from "@/view/TableView.vue";

export default {
  // registering
  components: { TableView },
  data() {
    return {
      items: [],
    };
  },
  // lifecycle hooks
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => {
        this.items = data;
      })
      .catch((error) => {
        console.error(error);
      });
  },
};
</script>

<style>
.MDJAminDiv {
  z-index: 4444;
  position: fixed;
  bottom: 5%;
  left: 2%;
}

.MDJAmin {
  text-decoration: none;
   border-bottom: 1px dashed rgb(204, 204, 204); 
   border-top: 1px dashed rgb(204, 204, 204); 
  /* border-bottom: 1px dashed rgb(44, 44, 44);*/
  /* border-top: 1px dashed rgb(44, 44, 44);*/
  padding: 4px 0;
  /* color: rgba(44, 44, 44, 0.525);*/
  color: rgba(204, 204, 204, 0.414); 
  font-family: monospace;
  font-style: italic;
  font-size: 1.1em;
  transition: all 0.5s;
}

.MDJAmin:hover {
  /* color: #000000; */
  color: #c52766ff;
}
</style>
