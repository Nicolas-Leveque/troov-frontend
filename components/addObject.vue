<template>
  <form @submit.prevent="createObj" method="POST" class="flex flex-col items-center min-w-full px-24 my-20">
    <div class="min-w-full">
      <label for="name" class="sr-only">Nom</label>
      <input type="text" id="name" name="name" v-model="name" placeholder="nom" class="rounded-t relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <div class="min-w-full">
      <label for="description" class="sr-only">Description</label>
      <input type="text" id="description" name="description" v-model="description" placeholder="description" class="relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <div class="min-w-full">
      <label for="image" class="sr-only">Description</label>
      <input type="file" id="image" name="image" @change="handleFileUpload" class="rounded-b relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm">
    </div>
    <button type="submit" class="w-1/2 mx-2 mt-5 py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Envoyer</button>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        description: '',
        image: ''
      }
    },
    methods: {
      async createObj() {
        let formData = new FormData()
        formData.append('name', this.name)
        formData.append('description', this.description)
        formData.append('image', this.image)
        formData.append('userId', localStorage.getItem('userId'))
        await this.$axios.$post('/object', formData, {
          headers:{
            'Content-Type': 'multipart/form-data'
          }
        })
        await this.$nuxt.refresh()
      },
      handleFileUpload( event ) {
        this.image = event.target.files[0]
      },
    }
  }
</script>
