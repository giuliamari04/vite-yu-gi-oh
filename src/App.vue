
<template>
  <div>
    <HeaderComponent />
    <main>
      <div class="container d-flex flex-wrap p-0 m-auto ">
        <div v-for="card in store.cardList" :key="card.id" class="my-w">
             <CardsComponent 
            :img="card.card_images[0].image_url_small"
            :name="card.name"
            :species="card.archetype"
          />
          </div>
         
        </div>
    </main>
  </div>
</template>
  
 <script>
 import { store } from './components/data/store';
 
 import HeaderComponent from './components/HeaderComponent.vue';
 import CardsComponent from './components/CardsComponent.vue';
 import axios from 'axios';
 export default {
   name: 'App',
   components: {
     HeaderComponent,
     CardsComponent,
   },
   data() {
     return {
       store,
     };
   },
   methods: {
     getCards() {
       axios.get(store.apiUrl).then((response) => {
        //console.log(response);
      store.cardList = response.data.data;
       });
     },
   },
   created() {
     this.getCards();
   }
 };
 </script>
 
 <style lang="scss" scoped>
 .container{
  background-color: blue;
 }
 </style>
 