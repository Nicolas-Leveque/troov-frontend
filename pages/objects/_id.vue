<template>
  <div class="flex flex-col items-center min-h-screen bg-gray-50">
    <p v-if="$fetchState.pending">...Chargement</p>
    <div v-else class="m-5">
      <h1 class="mb-52">{{objet.name}}</h1>
      <div class="flex justify-evenly mb-10 items-center">
        <nuxt-img :src="objet.imageUrl" class="rounded-xl mr-5 "/>
        <p>{{objet.description}}</p>
      </div>
      <div class="flex justify-evenly">
        <button @click="goBack" class="py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Retour</button>
        <button @click="showForm = !showForm" class="py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Modifier</button>
      </div>
      <ModifyObject :objet="objet" v-if="showForm" />
    </div>
  </div>
</template>
<script>
  import ModifyObject from "../../components/modifyObject";
  export default {
    components: {ModifyObject},
    data() {
      return {
        objet: {},
        showForm: false
      }
    },
    async fetch() {
      this.objet = await this.$axios.$get(`/object/${this.$route.params.id}`)
    },
    methods:{
      goBack() {
        return this.$router.go(-1)
      },

    }
  }
</script>
