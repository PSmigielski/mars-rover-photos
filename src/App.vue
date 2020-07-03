<template>
  <div class="rootWrapper">
    <h1>Mars rover photos</h1>
    <Background />
    <div class="searchBar">
      <Date v-model="date" :minDate="minDate" :maxDate="maxDate" @change="updateDate($event)"/>
      <Select v-model="roverName" @input="check()"/>
      <button @click="handleClick()">click</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import Background from './components/Background.vue';

import Select from './components/selectInput.vue';

import Date from './components/dateInput.vue';

const Api = 'https://api.nasa.gov/mars-photos/api/v1/rovers/';

export default {
  name: 'App',
  components: {
    Background,
    Select,
    Date,
  },
  data() {
    return {
      date: '',
      roverName: '',
      minDate: '',
      maxDate: '',
    };
  },
  methods: {
    check() {
      // const month = today.getMonth() + 1;
      // const day = today.getDate();
      // if (month < 10) month = `0${month}`;
      // if (day < 10) day = `0${day}`;
      if (this.roverName === 'curiosity') {
        this.minDate = '2012-08-06';
      //   this.maxDate = `${today.getFullYear()}-${month}-${day}`;
      //   console.log(`${today.getFullYear()}-${month}-${day}`);
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
          console.log(Response);
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
    align-items: center;
    justify-content: space-around;
  }
  h1{
    color:white;
    margin:0px;
  }
</style>
