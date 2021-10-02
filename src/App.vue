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
        label="Filter by type"
        :options="[
          { id: 1, name: `Waitlist` },
          { id: 2, name: `Student` },
          { id: 3, name: `None` },
        ]"
      />
      <span style="margin-left:5px;" />
      <Select
        label="Filter by postcode"
        :options="[
          { id: 1, name: 2000 },
          { id: 2, name: 2001 },
          { id: 3, name: `None` },
        ]"
      />
      <span style="margin-left:5px;" />
      <Select
        label="Sort by"
        :options="[
          { id: 1, name: `Id` },
          { id: 2, name: `Type` },
        ]"
      />
    </div>
  </div>
</template>

<script>
import Select from "./components/Select.vue";

export default {
  name: "App",
  components: { Select },
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
