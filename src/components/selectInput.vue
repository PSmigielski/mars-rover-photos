<template>
    <select class="select" :value="value" @input="handleChange" required>
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
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400&display=swap');
.select{
  width: 40%;
  height: 100%;
  text-align: center;
  border: 2px solid rgb(136, 134, 134);;
  border-left: none;
  border-right: none;
}
</style>
