<script>
import {ref, watch} from "vue";

export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  setup(props) {
    const selectAll = ref(false);

    const selectAllItems = () => {
      props.items.forEach(item => {
        item.selected = selectAll.value;
      });
    };

    watch(selectAll, selectAllItems);

    return {
      selectAll,
      selectAllItems,
    };
  },
};
</script>
<template>
  <table>
    <thead>
    <tr>
      <th><input type="checkbox" v-model="selectAll" @change="selectAllItems"/> Account</th>
      <th>ID</th>
      <th>Name</th>
      <th>City</th>
      <th>Email</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in items" :key="index">
      <td><input class="check" type="checkbox" v-model="item.selected"/> {{ item.username }}</td>
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.address.city }}</td>
      <td>{{ item.email }}</td>
    </tr>
    </tbody>
  </table>
</template>

<!--collapse = make iy cleaner-->

<style scoped>
thead tr th {
  background-color: #ae4a4a85;
}

table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: left;
}

th {
  background-color: #f0f0f0;
}
</style>