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
import axios from "axios";

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
      filterValue: "tutti",
      isLoading: true,
      error:"",
    };
  },

  methods: {
   
  updateFilter(value) {
      this.filterValue = value;
    },
    getCards() {
      store.error='';
       axios.get(store.apiUrl).then((response) => {
        //console.log(response);
        store.cardList = response.data.data;
        console.log(this.store.cardList);

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
      }).catch((error)=>{
        console.log(error)
        this.store.error = error.message;
      }).finally(() => {
        this.isLoading = false;
      });
    },
    filteredArchetypeList() {
      return this.store.cardList.filter(
        (card) => card.archetype.trim() === this.filterValue.trim()
      );
    },
    filteredCards() {
      if (this.filterValue === "tutti") {
        return this.store.cardList;
      } else {
        return this.store.cardList.filter(
          (card) => card.archetype === this.filterValue
        );
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
