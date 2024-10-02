<script >
export default {
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      selectAll: false
    };
  },
  methods: {
    selectAllItems() {
      this.items.forEach(item => {
        item.selected = this.selectAll;
      });
    }
  }
};
</script>

<template>
  <table>
    <thead>
    <tr>
      <th><input type="checkbox" v-model="selectAll" @change="selectAllItems"/> Account </th>
      <th>ID</th>
      <th>Name</th>
      <th>City</th>
      <th>Email</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in items" :key="index">
      <td><input class="check" type="checkbox" v-model="item.selected"/> {{item.username}} </td>
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.address.city}}</td>
      <td>{{item.email}}</td>
    </tr>
    </tbody>
  </table>
</template>

<style scoped>
thead tr th{
  background-color: black;
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