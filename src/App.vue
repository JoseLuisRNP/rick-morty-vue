<template>
  <div id="app" class="bg-yellow-200">
    <Header />
    <div class="flex justify-center p-3">
      <label for="search" class="font-main font-xl text-teal-700 my-2 mx-4">Search your</label>
      <input 
        type="text" 
        name="search"
        placeholder="Character" 
        :value="filterCharacter" 
        @input="setFilter" 
        class="text-center"
      />
    </div>    
    <list-characters :characters="characters" />
    <div class="text-center">
      <button class="px-4 py-2 bg-teal-700 text-white rounded-full" v-if="infoPagination.prev" @click="goToPrev">Prev</button>
      <button class="px-4 py-2 bg-teal-700 text-white rounded-full" v-if="infoPagination.next" @click="goToNext">Next</button>
    </div>
        
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import ListCharacters from "./components/ListCharacters.vue";
import "@/assets/index.css";

export default {
  name: "App",
  components: {
    Header,
    ListCharacters
  },
  data() {
    return {
      characters: [],
      filterCharacter: "",
      infoPagination: {}
    };
  },
  methods: {
    setFilter(e) {
      this.filterCharacter = e.target.value;
    },
    async goToNext() {
      const response = await fetch(this.infoPagination.next);
      const characters = await response.json();
      this.characters = characters.results;
      this.infoPagination = characters.info;
    },
    async goToPrev() {
      const response = await fetch(this.infoPagination.prev);
      const characters = await response.json();
      this.characters = characters.results;
      this.infoPagination = characters.info;
    }
  },
  watch: {
    filterCharacter: async function(newFilter) {
      const response = await fetch(`https://rickandmortyapi.com/api/character/?name=${newFilter}`);
      const characters = await response.json();
      this.characters = characters.results;
      this.infoPagination = characters.info;
    }
  },
  async created() {
    const response = await fetch("https://rickandmortyapi.com/api/character/");
    const characters = await response.json();
    this.characters = characters.results;
    this.infoPagination = characters.info;
  }
};
</script>
