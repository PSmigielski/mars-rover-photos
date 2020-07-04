<template>
  <div class="outerWrapper">
    <div class="detailsWrapper">
      <div class="image">
        <img :src="photo" />
      </div>
      <div class="content">
        <h1>sol: {{ sol }}</h1>
        <p>{{ camera }}</p>
      </div>
      <div class="close" @click="$emit('closeDetails')">
        <div class="close-left" />
        <div class="close-right" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Details',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      sol: null,
      camera: null,
    };
  },
  mounted() {
    this.photo = this.item.img_src;
    this.sol = this.item.sol;
    this.camera = this.item.camera.full_name;
  },
};
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
.outerWrapper {
  background: #f6f6f6;
  max-width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
}
.detailsWrapper {
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background-color:white;
}
.close {
  position: absolute;
  width: 30px;
  height: 30px;
  padding: 30px;
  right: 0;
  top: 0;
  cursor: pointer;
  &::before, &::after {
    position: absolute;
    top: 30px;
    right: 20px;
    content: '';
    width: 20px;
    height: 2px;
    background: black;
    display: block;
  }
  &::before {
    transform: rotate(45deg);
  }
  &::after {
    transform: rotate(-45deg);
  }
}
.image {
  width: 60%;
  max-height: 100%;
  img {
    height: auto;
    width: 100%;
   }
}
.content {
  width: 45%;
  height: 90%;
}
p{
  color: black;
  font-family: 'Poppins', sans-serif;
  font-weight: 300;
  font-size: 20px;
}
h1{
  color: #1f2e2c;
  font-family: 'Poppins', sans-serif;
  font-weight: 400;
}
 @media (min-width: 1024px) {
    .outerWrapper{
      max-width: 70%;
      height: 70%;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
    }
    .detailsWrapper{
      flex-direction: row;
    }
    .image {
      min-width: 50%;
      margin-right: 20px;
    }
 }
</style>
