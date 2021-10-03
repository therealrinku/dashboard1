<template>
  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Postcode</th>
        <th>Type</th>
        <th>Comments</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="data in sortedTableData()" :key="data.id">
        <td>{{ data.id }}</td>
        <td>{{ data.postcode }}</td>
        <td>{{ data.type }}</td>
        <td>{{ data.comments }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Table",
  props: {
    tableData: Array,
    filterByType: String,
    filterByPostcode: Number,
    sortBy: String,
    searchQuery: String,
  },
  methods: {
    sortedTableData() {
      return this.tableData
        .filter((enq) => enq.type.includes(this.filterByType))
        .filter((enq) =>
          enq.postcode.toString().includes(this.filterByPostcode)
        )
        .filter((enq) =>
          enq.comments
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase().trim())
        )
        .sort((a, b) => {
          switch (this.sortBy) {
            case "Id":
              return a.id - b.id;
            case "Type":
              return a.type.localeCompare(b.type);
          }
        });
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
  border: solid 1px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  border-collapse: collapse;
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.2);
  border-style: hidden;
}

table,
tr,
td,
th {
  text-align: left;
  padding: 10px;
}

tr {
  border-top: solid 1px rgba(0, 0, 0, 0.2);
}

th {
  font-weight: normal;
  text-transform: uppercase;
  border-bottom: solid 1px rgba(0, 0, 0, 0.2);
}

th {
  font-size: 13px;
}

td {
  font-size: 14px;
}
</style>
