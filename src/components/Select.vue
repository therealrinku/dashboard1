<template>
  <div>
    <p style="font-size:13px;margin-bottom:3px;">{{ label }}</p>
    <select>
      <option :key="option.id" v-for="option in options">{{
        option.name
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
  },
};
</script>

<style scoped>
select {
  border: solid 1px rgba(0, 0, 0, 0.2);
  padding: 7px 10px 7px 7px;
  width: 350px;
  outline: none;
  border-radius: 5px;
  background: white;
}
</style>
