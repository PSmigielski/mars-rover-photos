<template>
    <select :value="value" @input="handleChange">
      <option disabled value="">Please select rover</option>
      <option>curiosity</option>
      <option>opportunity</option>
      <option>spirit</option>
    </select>
</template>

<script>
// import { bus } from "../main";

export default {
  name: 'Select',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
