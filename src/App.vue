<template>
  <div class="rootWrapper">
    <Content />
    <Background />
    <div class="searchBar">
      <Date v-model="date" :minDate="minDate" :maxDate="maxDate" @change="updateDate($event)"/>
      <Select v-model="roverName" @input="check()"/>
      <button class="submitButton" @click="handleClick()">click</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import Background from './components/Background.vue';

import Select from './components/selectInput.vue';

import Date from './components/dateInput.vue';

import Content from './components/Content.vue';

const Api = 'https://api.nasa.gov/mars-photos/api/v1/rovers/';

export default {
  name: 'App',
  components: {
    Background,
    Select,
    Date,
    Content,
  },
  data() {
    return {
      date: '',
      roverName: '',
      minDate: '',
      maxDate: '',
      results: [],
    };
  },
  methods: {
    check() {
      // @todo add date obj
      if (this.roverName === 'curiosity') {
        this.minDate = '2012-08-06';
      } else if (this.roverName === 'opportunity') {
        this.minDate = '2004-01-25';
        this.maxDate = '2018-06-10';
      } else if (this.roverName === 'spirit') {
        this.minDate = '2004-01-04';
        this.maxDate = '2010-03-22';
      }
    },
    handleClick() {
      axios.get(`${Api}${this.roverName}/photos?earth_date=${this.date}&api_key=DEMO_KEY`)
        .then((Response) => {
          this.results = Response.data.photos;
          console.log(this.results);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    updateDate(updatedDate) {
      this.date = updatedDate;
    },
  },
};
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400&display=swap');
  .rootWrapper{
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .searchBar{
    margin: 30px 0px 0px 0px;
    display: flex;
    width: 500px;
    height: 60px;
    align-items: center;
    justify-content: space-around;
    .submitButton{
      width: 20%;
      height: 100%;
      font-size: 20px;
      font-family: 'Noto Sans JP', sans-serif;
      border: 2px solid rgb(136, 134, 134);
      transition: all 0.3s ease-in-out;
      &:hover{
        background-color: rgb(172, 170, 170);
      }
    }
    @media screen and (max-width:600px){
      width: 400px;
    }
  }
</style>
