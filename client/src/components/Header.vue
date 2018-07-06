<template>
  <v-toolbar fixed class="cyan" dark>
    <v-toolbar-title class="mr-4">
      <span class="home" @click="navigateTo({name: 'root'})"> TabTracker </span>
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn @click="navigateTo({name: 'Songs'})" flat dark>
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn v-if="!$store.state.isUserLoggedIn" @click="navigateTo({name: 'Login'})" flat dark>
        Login
      </v-btn>

      <v-btn v-if="!$store.state.isUserLoggedIn" @click="navigateTo({name: 'Register'})" flat dark>
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
    navigateTo (route) {
      this.$router.push(route)
    },
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({ name: 'root' })
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
