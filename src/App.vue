<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>vue-auth0</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat>
        <span class="mr-2" v-if="!authenticated" @click="auth.login()">Log in</span>
        <span class="mr-2" v-if="authenticated" @click="auth.logout()">Log out</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <v-container fluid>
        <router-view
          :auth="auth"
          :authenticated="authenticated">
        </router-view>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import AuthService from './auth/AuthService'

const auth = new AuthService()
const { login, logout, authenticated, authNotifier } = auth

export default {
  name: 'App',
  data () {
    authNotifier.on('authChange', authState => {
      this.authenticated = authState.authenticated
    })
    return {
      auth,
      authenticated
    }
  },
    methods: {
    login,
    logout
  }
}
</script>
