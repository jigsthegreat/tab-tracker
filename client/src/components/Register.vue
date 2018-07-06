<template>
  <v-layout>
    <v-flex xs6 offset-xs3>
      <panel title="Register">
        <form name="tab-tracker-form" autocomplete="off">
          <v-text-field type="email" label="E-mail" v-model="email"></v-text-field>
          <v-text-field type="password" label="Password" v-model="password" autocomplete="new-password"></v-text-field>
          <div class="error" v-html="error"></div>
          <v-btn class="cyan" @click="register" dark>Register</v-btn>
        </form>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  name: 'Register',
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        this.error = null
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* .error {
  color: red;
} */
</style>
