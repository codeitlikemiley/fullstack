<template>
  <v-app 
    v-cloak 
  >
    <home-nav-bar/>
    <v-content
      transition="slide-x-transition" 
      fluid
      pa-0
      ma-0
    >
      <nuxt/>
    </v-content>
    <footer-links/>
    <app-footer/>
  </v-app>
</template>

<script>
import AppFooter from '../partials/AppFooter.vue'
import HomeNavBar from '../partials/HomeNavBar.vue'
import FooterLinks from '../components/FooterLinks.vue'
export default {
    components: {
        AppFooter,
        HomeNavBar,
        FooterLinks
    }
}
</script>
