<template>
  <div
    v-if="active" 
    class="fixed top-0 left-0 h-full w-full bg-grey-transparent  flex justify-center content-center">
      <div class="relative flex flex-col bg-white rounded-md overflow-hidden my-auto">
        <a class="absolute p-4 bg-yellow-500 rounded-full text-white right-0 m-1" href="" @click.prevent="close">X</a>
        <img :src="info.image" :alt="info.name" />
        <div class="flex p-4 flex-col justify-around h-56">
          <p>Name: {{info.name}}</p>
          <p>Status: {{info.status}}</p>
          <p>Gender: {{info.gender}}</p>
          <p>Specie: {{info.species}}</p>
          <p>Type: {{typeCharacter}}</p>
          <p>Origin: {{info.origin.name}}</p>
          <p>Location: {{info.location.name}}</p>
        </div>
      </div>
    </div>
</template>
<script>
export default {
  props: [
    'info',
    'active'
  ],
  methods: {
    close() {
      this.$emit('close-modal');
    }
  },
  computed: {
    typeCharacter() {
      return this.info.type ? this.info.type : 'Normal'
    }
  }
  
}
</script>