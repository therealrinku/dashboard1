<template>
  <h2>Dashboard</h2>
  <input
    class="search-input"
    type="text"
    v-model="searchQuery"
    placeholder="Search for comment"
  />
</template>

<script>
export default {
  name: "App",
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
</style>
