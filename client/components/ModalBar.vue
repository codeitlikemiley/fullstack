<template>
  <v-dialog 
    v-model="dialog" 
    :overlay="false"
    fullscreen 
    transition="fade-transition" 
  >
    <v-card class="pt-0 blue-grey">
      <v-toolbar 
        dark 
        color="accent"
      >
        <v-spacer/>
        <v-toolbar-items>
          <fa 
            pull="right"
            class="mt-1 red--text text--lighten-4"
            icon="times" 
            style="cursor:pointer;"
            size="4x"
            @click="toggleNavBar()" 
          />
        </v-toolbar-items>
      </v-toolbar>

      <v-card-text style="padding-top:150px;">
        <v-container fluid>
          <v-layout
            v-if="!isAuthenticated"  
            row 
          >
            <v-flex 
              xs12 
              sm12 
              md4 
              offset-md4 
              lg4 
              offset-lg4 
              xl4 
              offset-xl4
              d-flex
            >
              <v-flex xs2>
                <fa 
                  size="3x" 
                  class="purple--text text--lighten-4" 
                  icon="sign-in-alt" 
                />
              </v-flex>
              <v-flex 
                xs10 
              >
                <span 
                  :class="[menuClass]" 
                  style="cursor:pointer;"
                  @click="goTo('login')"
                >
                  {{ login }}
                </span>
              </v-flex>
            </v-flex>
          </v-layout>
          <v-layout
            v-if="!isAuthenticated"
            row 
          >
            <v-flex 
              xs12 
              sm12 
              md4 
              offset-md4 
              lg4 
              offset-lg4 
              xl4 
              offset-xl4
              d-flex
            >
              <v-flex xs2>
                <fa 
                  size="3x" 
                  class="green--text text--lighten-2" 
                  icon="user-plus" 
                />
              </v-flex>
              <v-flex 
                xs10 
              >
                <span 
                  :class="[menuClass]" 
                  style="cursor:pointer;"
                  @click="goTo('register')"
                >
                  {{ register }}
                </span>
              </v-flex>
            </v-flex>
          </v-layout>
          <v-layout
            v-if="isAuthenticated"
            row 
          >
            <v-flex 
              xs12 
              sm12 
              md4 
              offset-md4 
              lg4 
              offset-lg4 
              xl4 
              offset-xl4
              d-flex
            >
              <v-flex xs2>
                <fa 
                  :class="[iconClass]" 
                  size="3x" 
                  icon="tachometer-alt" 
                />
              </v-flex>
              <v-flex 
                xs10 
              >
                <span 
                  :class="[menuClass]" 
                  style="cursor:pointer;"
                  @click="goTo('dashboard')"
                >
                  {{ dashboard }}
                </span>
              </v-flex>
            </v-flex>
          </v-layout>
          <v-layout
            row 
          >
            <v-flex 
              xs12 
              sm12 
              md4 
              offset-md4 
              lg4 
              offset-lg4 
              xl4 
              offset-xl4
              d-flex
            >
              <v-flex xs2>
                <fa 
                  size="3x" 
                  class="orange--text text--lighten-2" 
                  icon="life-ring" 
                />
              </v-flex>
              <v-flex 
                xs10 
              >
                <span 
                  :class="[menuClass]" 
                  style="cursor:pointer;"
                  @click="goTo('contact-us')"
                >
                  {{ support }}
                </span>
              </v-flex>
            </v-flex>
          </v-layout>
          <v-layout
            v-if="isAuthenticated"
            row 
          >
            <v-flex 
              xs12 
              sm12 
              md4 
              offset-md4 
              lg4 
              offset-lg4 
              xl4 
              offset-xl4
              d-flex
            >
              <v-flex xs2>
                <fa 
                  size="3x" 
                  class="red--text text--lighten-2" 
                  icon="sign-out-alt" 
                />
              </v-flex>
              <v-flex 
                xs10 
              >
                <span 
                  :class="[menuClass]" 
                  style="cursor:pointer;"
                  @click="logoutUser()"
                >
                  {{ logout }}
                </span>
              </v-flex>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import Bus from '../mixins/bus'
import { createNamespacedHelpers } from 'vuex'
const { mapState } = createNamespacedHelpers('auth')
export default {
    data: () => ({
        dialog: false,
        iconClass:{
            'info--text': true
        },
        menuClass:{
            'white--text': true,
            'display-1': true
        }
    }),
    computed: {
        ...mapState({
            isAuthenticated: 'token'
        }),
        login () {
            return this.$t('login')
        },
        logout () {
            return this.$t('logout')
        },
        register () {
            return this.$t('register')
        },
        dashboard () {
            return this.$t('dashboard')
        },
        support () {
            return this.$t('support')
        }
    },
    mounted(){
        Bus.$on('toggleNavBar', () => {
            this.dialog = !this.dialog
        })
    },
    methods: {
        goTo(route){
            this.$router.push({ name: route })
        },
        toggleNavBar(){
            this.dialog = !this.dialog
        },
        async logoutUser () {
            // Log out the user.
            await this.$store.dispatch('auth/logout')
            // Redirect to login.
            this.$router.push({ name: 'login' })
        }
    }
}
</script>

<style>

</style>
