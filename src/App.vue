<template>
  <div>
    <header>
      <HeaderComponent />
    </header>

    <main class="container">
      <SelectComponent 
        :filtervalue="filterValue"
        :ArchetypeList="store.ArchetypeList"
        @filter-change="updateFilter" />
     
      <div class="wrapper d-flex flex-wrap p-4 m-auto">
        <div class="w-100 bg-black text-light my-mx p-3">
          Found {{ filteredCards().length }} cards
        </div>

        <LoaderComponent  v-if="isLoading" />
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
import LoaderComponent from "./components/LoaderComponent.vue";
import SelectComponent from "./components/selectComponent.vue";
import axios, { AxiosError } from "axios";

export default {
  name: "App",
  components: {
    HeaderComponent,
    CardsComponent,
    LoaderComponent,
    SelectComponent,
  },
  data() {
    return {
      store,
      filterValue: "Alien",
      isLoading: true,
      currentPage: 1,
      cardsPerPage: 20,
    };
  },

  methods: {
    updateFilter(value) {
      this.filterValue = value;
      this.getCards();
    },

    getCards() {
      store.error = '';
      const offset = (this.currentPage - 1) * this.cardsPerPage;

      axios.get(store.apiUrl, {
        params: {
          num: this.cardsPerPage,
          offset: offset,
          archetype: this.filterValue,
        }
      }).then((response) => {
        store.cardList = response.data.data;

      }).catch((error) => {
        console.log(error)
        store.error = error.message;
      }).finally(() => {
        this.isLoading = false;
      });
      axios.get(store.apiUrl).then((response)=>{
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
    })
    },
    
    

    filteredCards() {
      let filteredList = this.store.cardList;

      if (this.filterValue !== "tutti") {
        filteredList = filteredList.filter((card) => card.archetype === this.filterValue);
      }

      const startIndex = (this.currentPage - 1) * this.cardsPerPage;
      const endIndex = startIndex + this.cardsPerPage;

      return filteredList.slice(startIndex, endIndex);
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
