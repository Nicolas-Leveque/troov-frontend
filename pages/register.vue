<template>
  <section class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8">
      <h2 class="text-center text-3xl">Register</h2>

      <Notication :message="error" v-if="error" />
      <form class="mt-8 space-y-6" @submit.prevent="register" method="POST">

        <div class="rounded-md shadow-sm -space-y-px">
          <div>
            <label for="nickname" class="sr-only">Nickname</label>
            <input id="nickname" name="nickname" type="text" v-model="nickname" required class="rounded-t relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Nickname">
          </div>
          <div>
            <label for="email-address" class="sr-only">Email address</label>
            <input id="email-address" name="email" type="email" v-model="email" required class="rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Email address">
          </div>
          <div>
            <label for="password" class="sr-only">Password</label>
            <input id="password" name="password" type="password" v-model="password" required class="rounded-b relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Password">
          </div>
        </div>
        <div>
          <button type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            Sign in
          </button>
        </div>
      </form>
      <div class="text-center mt-5" >
        Already got an account? <nuxt-link to="/login">Login</nuxt-link>
      </div>
    </div>
  </section>

</template>
<script>
  export default {
    auth: false,
    data() {
      return {
        nickname: '',
        email:'',
        password:'',
        error: null
      }
    },
    methods: {
      async register() {
        try {
          const user = await this.$axios.post('/user/signup', {
            nickname: this.nickname,
            email: this.email,
            password: this.password
          })
          localStorage.setItem('auth._token.local', `Bearer ${user.data.token}`)
          localStorage.setItem('userId', user.data.userId)
          this.$router.push('/content')

        } catch(e) {
          this.error = e.response.data.message
        }
      }
    }
  }
</script>
