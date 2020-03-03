<template>
  <div class="m-6 ">
    <img :src="info.image" alt="" class="rounded-full shadow-xl">
    <div class="text-center  bg-white p-6 rounded-lg shadow-xl">
      <h2 class="font-main text-center text-3xl">{{ info.name }}</h2>
      <h3 class="font-main text-center text-lg text-teal-700">{{ info.species }}</h3>
      <button
       @click="seeInfo"
       class="rounded-full bg-yellow-600 text-white px-4 py-2 mt-2">See info</button>
    </div>
  </div>
</template>
<script>


export default {
  props: [
    'info'
  ],
  methods: {
    seeInfo() {
      this.$emit('open-modal', this.info);
    }
  }
}
</script>