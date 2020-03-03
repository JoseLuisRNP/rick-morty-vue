<template>
  <div>
    <div class="flex flex-wrap justify-around">
        <character-card 
          :info="character"  
          @open-modal="openModal" 
          v-for="character in characters" 
          :key="character.id"
          />
        <character-info 
          :info="characterSelected" 
          :active="modalActive" 
          @close-modal="closeModal"
          />
      </div>
  </div>
</template>
<script>
import CharacterCard from "./CharacterCard.vue";
import CharacterInfo from "./CharacterInfo.vue";

export default {
  components: {
    CharacterCard,
    CharacterInfo
  },
  props: ["characters"],
  data() {
    return { 
      characterSelected: {},
      modalActive: false,
    }
  },
  methods: {
    openModal(character) {
      this.characterSelected = character;
      this.modalActive = true;

    },
    closeModal() {
      this.modalActive = false;
    }
  }
};
</script>