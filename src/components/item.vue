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
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        width: 300px;
        height: 300px;
        @media screen and (max-width:769px){
          width: 500px;
          height: 500px;
        }
        @media screen and (max-width:620px){
          width: 400px;
          height: 400px;
        }
        @media screen and (max-width:500px){
          width: 300px;
          height: 300px;
        }
    }
</style>
