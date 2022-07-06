<template>
  <main class="min-h-screen flex flex-col items-center justify-start bg-gray-50 py-12 px-4">
    <h1 class="font-bold mb-10 ">Bienvenue dans mon défi Troov! </h1>
    <nuxt-img
      src="/pexels-ovan-62689.jpg"
      width="500"
      height="500"
    />
    <p class="mt-5">Pour commencer à utiliser le site, veuillez vous connecter ou créer un compte</p>
    <div class="m-10">
      <NuxtLink to="/login" class="py-2 px-4 border-transparent rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Connection</NuxtLink>
      <NuxtLink to="/register" class="py-2 px-4 border-transparent rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Créer un compte</NuxtLink>
    </div>
  </main>
</template>
