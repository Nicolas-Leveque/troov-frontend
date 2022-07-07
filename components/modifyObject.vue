<template>
  <form @submit.prevent="modifyObj" method="PUT" class="m-10 flex flex-col items-center">
    <div class="min-w-full">
      <label for="name" class="sr-only">Nom</label>
      <input type="text" id="name" name="name" v-model="name" placeholder="nom" class="rounded-t relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <div class="min-w-full">
      <label for="description" class="sr-only">Description</label>
      <input type="text" id="description" name="description" v-model="description" placeholder="description" class="rounded-b relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <div class="min-w-full">
      <label for="image" class="sr-only">Description</label>
      <input type="file" id="image" name="image" @change="handleFileUpload( $event )" class="rounded-b relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <div class="flex justify-between">
      <button type="submit" class="w-3/4 mx-2 mt-5 py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Envoyer</button>
      <button @click="handleDelete" class="w-3/4 mx-2 mt-5 py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-red-600 hover:bg-redo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500">Supprimer</button>
    </div>
  </form>
</template>
<script>
export default {
  props: {
    objet: {}
  },
  data() {
    return {
      name: this.objet.name,
      description: this.objet.description,
      image: ''
    }
  },
  methods: {
    async modifyObj() {
      let formData = new FormData();
      formData.append('name', this.name)
      formData.append('description', this.description)
      formData.append('image', this.image)
      await this.$axios.$put(`/object/${this.objet._id}`, formData, {
        headers: {
          'Content-Type': 'multipart/form-data'
        }
      })
      this.$nuxt.refresh()
    },
    handleFileUpload( event ) {
      this.image = event.target.files[0]
    },
    async handleDelete() {
      await this.$axios.$delete(`/object/${this.objet._id}`)
      this.$router.push('/content')
    }
  }
}
</script>
