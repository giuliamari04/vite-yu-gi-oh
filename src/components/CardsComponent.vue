<template>
    <div class="card border-0 rounded-0">
    <img :src="img" class="card-img-top" :alt="name">
    <div class="card-body text-center">
      <h5 class="card-title text-light text-uppercase fw-bolder">{{ name }}</h5>
      <h5 class="card-title">{{ species }}</h5>
    </div>
  </div>

  <div class="col-12" v-if="store.error">
    <div class="alert-danger alert">
      {{ store.error }}
    </div>
  </div>
   </template>
   
   <script>
   import { store } from "./data/store";

export default {
  name: "CardsComponent",
  props: {
    img: String,
    name: String,
    species: String,
  },
  data() {
    return {
      store,
    };
  },
};
   </script>
   
   <style lang="scss" scoped>
   @use '../assets/styles/partials/variables' as *;
   .card{
    background-color: $bgYellow;
   }
   </style>