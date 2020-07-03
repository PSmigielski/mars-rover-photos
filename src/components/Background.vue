<template>
  <div class="backgroundWrapper" />
</template>
<script>
export default {
  name: 'Background',
};
</script>
<style lang="scss" scoped>
  .backgroundWrapper{
      background-image: url('../assets/background.jpg');
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      width: 100%;
      height: 100%;
      z-index: -1;
      top:0;
      position: fixed;
  }
</style>
