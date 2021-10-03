<template>
  <h2>Dashboard</h2>
  <input
    class="search-input"
    type="text"
    v-model="searchQuery"
    placeholder="Search for Comment"
  />

  <div class="toolbar">
    <h4>Sorting and Filtering</h4>
    <div class="toolbar-tools">
      <Select
        :onSelectChange="OnSelectChange"
        label="Filter by type"
        :options="[
          { id: 1, name: `` },
          { id: 2, name: `Student` },
          { id: 3, name: `Waitlist` },
        ]"
      />
      <span style="margin-left:5px;" />
      <Select
        :onSelectChange="OnSelectChange"
        label="Filter by postcode"
        :options="[
          { id: 1, name: `` },
          { id: 2, name: 2001 },
          { id: 3, name: 2000 },
        ]"
      />
      <span style="margin-left:5px;" />
      <Select
        :onSelectChange="OnSelectChange"
        label="Sort by"
        :options="[
          { id: 1, name: `Id` },
          { id: 2, name: `Type` },
        ]"
      />
    </div>
  </div>

  <div class="data-table">
    <h4>Enquiries &#183; page {{ pageNo }}</h4>
    <Table
      :tableData="enquiries"
      :sortBy="sortBy"
      :filterByPostcode="filterByPostcode"
      :filterByType="filterByType"
      :searchQuery="searchQuery"
    />
  </div>

  <div class="pagination-buttons">
    <button :disabled="pageNo === 1" @click="pageNo = 1">1</button>
    <button :disabled="pageNo === 2" @click="pageNo = 2">2</button>
  </div>
</template>

<script>
import Select from "./components/Select.vue";
import Table from "./components/Table.vue";
import data from "./data/enquiries.json";

export default {
  name: "App",
  components: { Select, Table },
  data() {
    return {
      searchQuery: "",
      enquiries: data.slice(0, 10).sort((a, b) => a.id - b.id),
      filterByType: "",
      filterByPostcode: 0,
      sortBy: "Id",
      pageNo: 1,
    };
  },
  methods: {
    OnSelectChange(type, value) {
      if (type === "Filter by type") {
        this.filterByType = value;
      }
      if (type === "Filter by postcode") {
        this.filterByPostcode = value;
      }
      if (type === "Sort by") {
        this.sortBy = value;
      }
    },
  },
  watch: {
    pageNo: function() {
      if (this.pageNo === 1) {
        this.enquiries = data.slice(0, 10);
      } else {
        this.enquiries = data.slice(10);
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");

#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  width: 85vw;
  margin: auto;
}

button:hover:not(:disabled) {
  cursor: pointer;
}

.search-input {
  border: solid 1px rgba(0, 0, 0, 0.2);
  padding: 7px 10px 7px 7px;
  width: 350px;
  outline: none;
  border-radius: 5px;
}

.search-input:focus {
  box-shadow: 0 0 0 0.5pt green;
}

.toolbar {
  margin-top: 35px;
}

.toolbar-tools {
  display: flex;
  align-items: center;
  margin-top: -15px;
  flex-wrap: wrap;
}

.pagination-buttons {
  margin: 25px 0;
  display: flex;
  justify-content: center;
}

.pagination-buttons button {
  padding: 10px 15px;
  border: solid 1px rgba(0, 0, 0, 0.2);
  background: inherit;
  border-radius: 5px;
}

.pagination-buttons button:hover:not(:disabled) {
  border: solid 1px green;
}

.pagination-buttons button:last-child {
  margin-left: 10px;
}
</style>
