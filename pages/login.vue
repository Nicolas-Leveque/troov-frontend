<template>
  <section class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8">
      <h2 class="text-center text-3xl">Login</h2>

      <Notication :message="error" v-if="error" />
      <form class="mt-8 space-y-6" @submit.prevent="login" method="POST">
        <div class="rounded-md shadow-sm -space-y-px">
          <div>
            <label for="email-address" class="sr-only">Email address</label>
            <input id="email-address" name="email" type="email" v-model="email" required class="rounded-t relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Email address">
          </div>
          <div>
            <label for="password" class="sr-only">Password</label>
            <input id="password" name="password" type="password" v-model="password" required class="rounded-b relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Password">
          </div>
        </div>
        <div>
          <button type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            Login
          </button>
        </div>
      </form>
      <div class="text-center mt-5" >
        Need an account? <nuxt-link to="/register">Register</nuxt-link>
      </div>
    </div>
  </section>

</template>

<script>
  export default {
    auth:  false ,
    data() {
      return {
        email:'',
        password:'',
        error: null
      }
    },
    methods: {
      async login() {
        try {
          const user = await this.$auth.loginWith('local', {
            data: {
              email: this.email,
              password: this.password
            }
          })
          console.log(user)
          await localStorage.setItem('auth._token.local', `Bearer ${user.data.token}`)
          this.$router.push('/content')
        } catch (e) {
          this.error = e.response.data.message
        }
      }
    }
  }
</script>
