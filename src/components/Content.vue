<template>
  <div class="contentWrapper">
    <h1>Mars rover photos</h1>
    <p>curiosity: 2012.08.06 to today</p>
    <p>opportunity: 2004.01.25 to 2018.06.10</p>
    <p>spirit: 2004.01.04 to 2010.03.22</p>
  </div>
</template>

<script>
export default {
  name: 'Content',
};
</script>

<style lang="scss" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400&display=swap');

    .contentWrapper{
        width: 350px;
        height: 350px;
        background-color: rgba(255, 255, 255, 0.55);
        text-align: center;
        display: flex;
        justify-content: center;
        font-family: 'Noto Sans JP', sans-serif;
        align-items: center;
        flex-direction: column;
        border-radius: 30px;
    }
    h1{
        color: rgba(0, 0, 0, 1);
        font-weight: 400;
    }
    p{
        color: rgba(0, 0, 0, 1);
        font-weight: 300;
        font-size:18px;
    }
</style>
