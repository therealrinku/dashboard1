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
    <h4>Enquiries(showing {{ filteredEnquiries.length }} enquiries)</h4>
    <Table :tableData="filteredEnquiries" />
  </div>
</template>

<script>
import Select from "./components/Select.vue";
import Table from "./components/Table.vue";
import enquiries from "./data/enquiries.json";

const Enquiries = enquiries.sort((a, b) => a.id - b.id);

export default {
  name: "App",
  components: { Select, Table },
  data() {
    return {
      searchQuery: "",
      filteredEnquiries: Enquiries,
      filterByType: "",
      filterByPostcode: 0,
      sortBy: "Id",
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

    FilterSearchAndSort() {
      this.filteredEnquiries = enquiries
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

  watch: {
    searchQuery: function() {
      this.FilterSearchAndSort();
    },
    filterByType: function() {
      this.FilterSearchAndSort();
    },
    filterByPostcode: function() {
      this.FilterSearchAndSort();
    },
    sortBy: function() {
      this.FilterSearchAndSort();
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
</style>
