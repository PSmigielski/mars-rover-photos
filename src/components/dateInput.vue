<template>
  <input type="date" name :value="value" :min="minDate" :max="maxDate" @change="handleDate" required>
</template>

<script>
export default {
  name: 'Date',
  props: {
    value: {
      type: String,
    },
    minDate: {
      type: String,
      default: '',
    },
    maxDate: {
      type: String,
      default: '',
    },
  },
  methods: {
    handleDate(e) {
      this.$emit('change', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
