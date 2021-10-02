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

  <div class="data-table">
    <h4>Enquiries(showing {{ filteredEnquiries.length }} enquiries)</h4>
    <Table :tableData="filteredEnquiries" />
  </div>
</template>

<script>
import Select from "./components/Select.vue";
import Table from "./components/Table.vue";

const enquiries = [
  {
    comments:
      "The black-footed cat is the smallest wild cat, at just 20 inches  long.",
    id: 39435,
    postcode: 2000,
    type: "Waitlist",
  },
  {
    comments:
      "Egg yolks are one of the few foods that naturally contain Vitamin  D.",
    id: 39436,
    postcode: 2001,
    type: "Waitlist",
  },
  {
    comments: "Peaches are the third most popular fruit grown in America.",
    id: 39437,
    postcode: 2000,
    type: "Waitlist",
  },
  {
    comments:
      "The fear of cooking is known as Mageirocophobia and is a  recognized phobia.",
    id: 39438,
    postcode: 2001,
    type: "Waitlist",
  },
  {
    comments:
      "1912 saw the last Olympic gold medals made entirely out of  gold.",
    id: 3939,
    postcode: 2000,
    type: "Waitlist",
  },
  {
    comments: "The only letter that doesn’t appear on the periodic table is J.",
    id: 39440,
    postcode: 2001,
    type: "Waitlist",
  },
  {
    comments:
      "A dog was the first living creature to be sent into space in  1957.",
    id: 39441,
    postcode: 2000,
    type: "Waitlist",
  },
  {
    comments: "Clinomania is the excessive desire to lay in bed all day.",
    id: 39442,
    postcode: 2001,
    type: "Waitlist",
  },
  {
    comments:
      "Red pandas have no living relatives – they aren’t even related to  giant pandas.",
    id: 39443,
    postcode: 2000,
    type: "Waitlist",
  },
  {
    comments:
      "After Christianity, the largest religious affiliation in the U.S.  is Judaism.",
    id: 39444,
    postcode: 2001,
    type: "Waitlist",
  },
  {
    comments: "Dogs have a total of 42 teeth when they are fully-grown.",
    id: 39445,
    postcode: 2001,
    type: "Student",
  },
  {
    comments: "The center of a comet is called a nucleus.",
    id: 39446,
    postcode: 2000,
    type: "Student",
  },
  {
    comments:
      "The Earth is the only planet in our solar system not named after  either a Greek or Roman God.",
    id: 39447,
    postcode: 2001,
    type: "Student",
  },
  {
    comments: "26 is the atomic number of iron.",
    id: 39448,
    postcode: 2000,
    type: "Student",
  },
  {
    comments: "If you keep a goldfish in a dark room, it will become pale.",
    id: 39449,
    postcode: 2001,
    type: "Student",
  },
  {
    comments:
      "The patterns on a giraffe are totally unique – no two giraffes  are ever the same.",
    id: 39450,
    postcode: 2000,
    type: "Student",
  },
  {
    comments: "A standard 12oz jar of honey take 864 bees to produce.",
    id: 39451,
    postcode: 2001,
    type: "Student",
  },
  {
    comments:
      "The first movie ever to put out a motion-picture soundtrack was  Snow White and the Seven Dwarves.",
    id: 39452,
    postcode: 2000,
    type: "Student",
  },
  {
    comments:
      "In general, people tend to read as much as 10% slower from a  screen than from paper.",
    id: 39453,
    postcode: 2001,
    type: "Student",
  },
  {
    comments:
      "The world’s longest place name has 85 letters & is located in New  Zealand.",
    id: 39454,
    postcode: 2000,
    type: "Student",
  },
];

export default {
  name: "App",
  components: { Select, Table },
  data() {
    return {
      searchQuery: "",
      filteredEnquiries: enquiries,
    };
  },
  watch: {
    searchQuery: function filterEnquiries() {
      this.filteredEnquiries = enquiries.filter((enq) =>
        enq.comments
          .toLowerCase()
          .includes(this.searchQuery.trim().toLowerCase())
      );
    },
  },
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
