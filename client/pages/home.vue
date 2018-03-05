<template>
  <v-layout 
    column 
    justify-center 
    align-center
  >
    <v-flex 
      xs12 
      sm8 
      md6
    >
      <div class="text-xs-center">
        <nuxt-logo/>
      </div>
      <v-card>
        <v-card-title class="headline">Welcome to Vuetified!</v-card-title>
        <v-card-text>
          
          <p>This is An Integration of Laravel, Nuxt and Vuetify</p>
          <p>For more information on Laravel, check out the 
            <a 
              href="https://laravel.com/docs/5.5" 
              target="_blank"
            >documentation</a>.
          </p>
          <p>For more information on Vuetify, check out the 
            <a 
              href="https://next.vuetifyjs.com/getting-started/quick-start" 
              target="_blank" 
              title="chat"
            >
              Documentation
            </a>.
          </p>
          <p>For more information on Nuxt, check out the 
            <a 
              href="https://nuxtjs.org/guide" 
              target="_blank" 
              title="contribute"
            >
              documentation
            </a>.
          </p>
          <p>Thank you for developing with Vuetified and I look forward to bringing more exciting features in the future.</p>
          <div class="text-xs-right">
            <em><small>&mdash; Uriah Galang</small></em>
          </div>
          <hr class="my-3">
          <h2>Users List Using GraphQL</h2>
          <div 
            v-for="(user,key) in users" 
            :key="key"
          >
            <p>ID: {{ user.id }}</p>
            <p>NAME: {{ user.name }}</p>
            <p>EMAIL: {{ user.email }}</p>
          </div>
          <hr class="my-3">
          <a 
            href="https://github.com/codeitlikemiley/vuetified" 
            target="_blank"
          >
            Clone Repo
          </a>
          <br>
          <a 
            href="https://facebook.com/uriah.san" 
            target="_blank"
          >
            Follow Me On Facebook
          </a>
        </v-card-text>
        <v-card-actions>
          <v-spacer/>
          <v-btn 
            color="primary" 
            flat 
            nuxt 
            to="/inspire"
          >
            Read Documentation
          </v-btn>
        </v-card-actions>
          
      </v-card>
    </v-flex>
  </v-layout>
</template>


<script>
import NuxtLogo from '../components/NuxtLogo.vue'
import FetchUsers from '../graphql/fetchUsers.gql'

export default {
    components: {
        NuxtLogo
    },
    //! Ensure We Have the Users Data before We Render
    async asyncData ({app}) {
        let client = app.apolloProvider.defaultClient
        let { data } = await client.query({
            query: FetchUsers,
            update: data => data.Users
        })
        return {
            users: data.Users
        }
    },
    layout: 'home',
    head () {
        return { title: this.$t('home') }
    }
    
}
</script>
