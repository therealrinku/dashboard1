<template>
  <div>
    <p style="font-size:13px;margin-bottom:3px;">{{ label }}</p>
    <select @change="Changed($event)">
      <option :key="option.id" v-for="option in options" :value="option.name">{{
        option.name || `None`
      }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    label: String,
    options: Array,
    onSelectChange: Function,
  },
  methods: {
    Changed(e) {
      this.onSelectChange(this.label, e.target.value);
    },
  },
};
</script>

<style scoped>
select {
  border: solid 1px rgba(0, 0, 0, 0.2);
  padding: 7px 10px 7px 7px;
  width: 150px;
  outline: none;
  border-radius: 5px;
  background: white;
}

select:focus {
  box-shadow: 0 0 0 0.5pt green;
}
</style>
