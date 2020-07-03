<template>
  <div class="rootWrapper">
    <h1>Mars rover photos</h1>
    <Background />
  </div>
</template>

<script>
import Background from './components/Background.vue';

export default {
  name: 'App',
  components: {
    Background,
  },
};
</script>

<style lang="scss" scoped>
  .rootWrapper{
    width: 100vw;
    height: 100vh;
  }
  h1{
    margin:0px;
  }
</style>
