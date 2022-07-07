<template>
  <div class="flex flex-col items-center bg-gray-50 min-h-screen p-14">
    <h1 class="mb-20 justify-self-start">Liste des objets</h1>
    <p v-if="$fetchState.pending">...Chargement</p>
    <p v-else-if="$fetchState.error">Une erreur est survenue pendant le chargement des objets</p>
    <ul v-else class="flex flex-wrap w-full justify-center">
      <li v-for="object in objects" :key="object._id" class="min-w-max w-1/4 h-32 border border-black rounded-md m-3 p-3">
        <NuxtLink :to="{ name: 'objects-id', params: { id: object._id} }" class="flex items-center" no-prefetch>
          <nuxt-img :src="object.imageUrl" width="80" height="80" class="m-2 rounded-full"/>
          <h3 class="underline decoration-wavy">{{object.name}}</h3>
        </NuxtLink>
      </li>
    </ul>
    <button @click="showForm = !showform">Ajouter un objet</button>
    <add-object v-if="showForm"/>
  </div>
</template>
<script>
export default {
  components: {},

  data() {
    return {
      objects: [],
      showForm: false
    }
  },
  async fetch() {
    this.objects = await this.$axios.$get('/object')
  }

}
</script>
