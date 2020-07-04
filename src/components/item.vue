<template>
    <div :style="style" class="item" />
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.img_src,
    };
  },
  computed: {
    style() {
      return `background: url('${this.photo}')`;
    },
  },
};
</script>

<style lang="scss" scoped>
    .item{
        background-position: 50% 50%;
        background-repeat: no-repeat;
        background-size: cover;
        width: 300px;
        height: 300px;
    }
</style>
