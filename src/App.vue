<template>
  <div class="rootWrapper">
    <Content v-if="state===0" />
    <transition name="fade-out">
      <Background v-if="state===0" />
    </transition>
    <div class="searchBar" :class="state ? 'start' : ''">
      <Date v-model="date" :minDate="minDate" :maxDate="maxDate" @change="updateDate($event)"/>
      <Select v-model="roverName" @input="check()"/>
      <button class="submitButton" @click="handleClick()">click</button>
    </div>
    <div class="results" >
      <p v-if="results.length === 0 && state === 1" class="notFound">there are no photos here</p>
      <Item v-for="item in results" :item="item" :key="item.id" @click.native="handleDetailsOpen(item)" />
    </div>
    <Details v-if="detailsOpen" :item="detailsItem" @closeDetails="detailsOpen = false" />
  </div>
</template>

<script>
import axios from 'axios';

import Background from './components/Background.vue';

import Details from './components/Details.vue';

import Item from './components/item.vue';

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
    Item,
    Details,

  },
  data() {
    return {
      detailsOpen: false,
      detailsItem: null,
      date: '',
      loading: false,
      roverName: '',
      minDate: '',
      maxDate: '',
      state: 0,
      results: [],
    };
  },
  methods: {
    handleDetailsOpen(item) {
      this.detailsOpen = true;
      this.detailsItem = item;
    },
    check() {
      if (this.roverName === 'curiosity') {
        this.minDate = '2012-08-06';
        this.maxDate = '';
      } else if (this.roverName === 'opportunity') {
        this.minDate = '2004-01-25';
        this.maxDate = '2018-06-10';
      } else if (this.roverName === 'spirit') {
        this.minDate = '2004-01-04';
        this.maxDate = '2010-03-22';
      }
    },
    handleClick() {
      this.loading = true;
      axios.get(`${Api}${this.roverName}/photos?earth_date=${this.date}&api_key=DEMO_KEY`)
        .then((Response) => {
          this.state = 1;
          this.loading = false;
          this.results = Response.data.photos;
          console.log(this.results);
        })
        .catch((e) => {
          console.table(e);
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
  .fade-out-enter-active, .fade-out-leave-active {
    transition: opacity .2s ease-in-out;
  }
  .fade-out-enter, .fade-out-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
  .rootWrapper{
    min-width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    overflow-x: hidden;
  }
  .notFound{
    text-align: center;
    width: 100%;
  }
  .searchBar{
    margin: 30px 0px 0px 0px;
    display: flex;
    width: 500px;
    height: 60px;
    align-items: center;
    justify-content: space-around;
    &.start{
      justify-self: start;
      margin-bottom: 50px;
    }
    .submitButton{
      width: 20%;
      height: 100%;
      font-size: 20px;
      font-family: 'Noto Sans JP', sans-serif;
      transition: all 0.3s ease-in-out;
      border:2px solid rgb(136, 134, 134);
      border-left: none;
      &:hover{
        background-color: rgb(172, 170, 170);
      }
    }
    @media screen and (max-width:600px){
      width: 400px;
    }
  }
  .results{
    align-items: center;
    justify-items: center;
    width: 80%;
    display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
    @media screen and (max-width:1520px){
      grid-template-columns: 1fr 1fr 1fr ;
    }
    @media screen and (max-width:1170px){
      grid-template-columns: 1fr 1fr;
    }
    @media screen and (max-width:768px){
      grid-template-columns: 1fr;
    }
  }
</style>
