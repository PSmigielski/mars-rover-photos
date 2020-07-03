<template>
  <div class="rootWrapper">
    <h1>Mars rover photos</h1>
    <Background />
    <div class="searchBar">
      <input type="date" v-model="date" :min="minDate" :max="maxDate" required>
      <select v-model="roverName" @change="check()">
          <option disabled value="">Please select rover</option>
          <option>curiosity</option>
          <option>opportunity</option>
          <option>spirit</option>
      </select>
      <button @click="handleClick()">click</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import Background from './components/Background.vue';

const Api = 'https://api.nasa.gov/mars-photos/api/v1/rovers/';

export default {
  name: 'App',
  components: {
    Background,
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
      console.log(this.roverName);
      if (this.roverName === 'curiosity') this.minDate = '2012-08-06';
      else if (this.roverName === 'opportunity') {
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
  }
  h1{
    color:white;
    margin:0px;
  }
</style>
