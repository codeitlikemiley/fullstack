<template>
  <v-toolbar 
    color="accent" 
    fixed 
    app
  >
    <!-- Title -->
    <v-toolbar-title>
      <v-avatar>
        <img 
          :src="logo" 
          alt="logo"
        >
      </v-avatar>
      <span :class="[titleClass]">{{ title }}</span>
    </v-toolbar-title>
    <!-- center logo -->
    <v-spacer/>
    <v-toolbar-items>
      <locale-dropdown 
        text-color="white--text" 
        icon-color="info--text"
        text-size="headline"
        icon-size="2x"
      />
    </v-toolbar-items>
    <fa 
      :class="[iconClass]" 
      pull="right" 
      icon="bars" 
      size="3x"
      style="cursor:pointer;"
      @click="toggleNavBar"
    />
    <modal-bar/>
  </v-toolbar>
  
</template>

<script>
import { VAvatar } from 'vuetify'
import LocaleDropdown from '../components/LocaleDropdown'
import ModalBar from '../components/ModalBar'
import Bus from '../mixins/bus'

export default {
    components: {
        LocaleDropdown,
        VAvatar,
        ModalBar
    },
    data: () => ({
        titleClass: {
            'white--text': true,
            'headline': true
        },
        iconClass: {
            'info--text': true
        }
    }),
    computed: {
        title () {
            return this.$env.APP_NAME
        },
        logo () {
            return '/v.png'
        }
    },
    methods: {
        toggleNavBar(){
            Bus.$emit('toggleNavBar')
        }
    }
}
</script>

<style>

</style>
