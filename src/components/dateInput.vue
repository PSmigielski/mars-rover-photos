<template>
  <input type="date" class="dateInput" name="dateInput" :value="value" :min="minDate" :max="maxDate" @change="handleDate" required>
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
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400&display=swap');
.dateInput{
  width: 40%;
  height: 54px;
  text-align: center;
  font-size: 25px;
  border: 2px solid rgb(136, 134, 134);
  @media screen and (max-width:600px){
    font-size: 20px;
  }
}
</style>
