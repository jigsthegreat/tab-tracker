<template>
  <v-toolbar fixed class="cyan" dark>
    <v-toolbar-title class="mr-4">
      <router-link tag="span" class="home" :to="{name: 'Songs'}"> TabTracker </router-link>
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn :to="{name: 'Songs'}" flat dark>
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn v-if="!$store.state.isUserLoggedIn" :to="{name: 'Login'}" flat dark>
        Login
      </v-btn>

      <v-btn v-if="!$store.state.isUserLoggedIn" :to="{name: 'Register'}" flat dark>
        Sign Up
      </v-btn>

      <v-btn v-if="$store.state.isUserLoggedIn" @click="logout" flat dark>
        Logout
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {

    }
  },
  methods: {
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({ name: 'Songs' })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .home {
    cursor: pointer;
  }

  .home:hover {
    color: #342345;
  }
</style>
