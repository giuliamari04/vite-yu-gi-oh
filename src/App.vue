<template>
  <div>
    <header>
      <HeaderComponent />
    </header>

    <main class="container">
      <select
        class="form-select w-25 my-3"
        aria-label="Default select example"
        v-model="filtervalue"
        @click="getCards()"
      >
      <option value="tutti"> tutti</option>
        <option
          v-for="option in store.ArchetypeList"
          :key="option.id"
          :value="option.archetype"
        >
          {{ option.archetype }}
        </option>
      </select>
      <div class="wrapper d-flex flex-wrap p-4 m-auto">
        <div class="w-100 bg-black text-light my-mx p-3">prova</div>
        <div v-for="card in filteredCards()" :key="card.id" class="my-w mt-0">
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
import { store } from "./components/data/store";

import HeaderComponent from "./components/HeaderComponent.vue";
import CardsComponent from "./components/CardsComponent.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    HeaderComponent,
    CardsComponent,
  },
  data() {
    return {
      store,
      filtervalue:"tutti",
    };
  },

  methods: {
    getCards() {
      axios.get(store.apiUrl).then((response) => {
        //console.log(response);
        store.cardList = response.data.data;
        console.log( this.store.cardList);

        const uniqueArchetypes = new Set();
        response.data.data.forEach((card) => {
          if (card.archetype && card.archetype.trim() !== "") {
            uniqueArchetypes.add(card.archetype.trim());
          }
        });
       
        store.ArchetypeList = [...uniqueArchetypes].map((archetype, id) => ({
          id,
          archetype,
        }));
        console.log(this.store.ArchetypeList);
      });
    },
    filteredArchetypeList() {
      return this.store.cardList.filter(
      (card) => card.archetype.trim() === this.filtervalue
     
    ); 
    
    },
    filteredCards(){
      if(this.filtervalue === "tutti"){
        return this.store.cardList;
      }else{
        return this.store.cardList.filter(card => card.archetype === this.filtervalue);
      }
      
       },
     
  },
  created() {
    this.getCards();
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  background-color: white;
}

.my-mx {
  margin-left: 20px;
  margin-right: 20px;
}
</style>
