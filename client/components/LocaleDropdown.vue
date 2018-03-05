<template>
  <v-menu>
    <v-btn 
      slot="activator"
      flat 
      color="white"
    >
      <img 
        :class="[textColor,textSize]" 
        :src="currentLocale"
        width="32px"
      >
      <fa 
        :class="[iconColor]"
        :size="iconSize"
        pull="right" 
        icon="caret-down" 
      />
    </v-btn>
    <v-list>
      <v-list-tile 
        v-for="(value, key) in locales" 
        :key="key" 
        @click="setLocale(key)"
      >
        <img 
          :class="[textColor,textSize]" 
          :src="value"
          width="32px"
        >
      </v-list-tile>
    </v-list>
  </v-menu>
</template>

<script>
import { VMenu } from 'vuetify'
import { mapGetters } from 'vuex'
import { loadMessages } from '~/plugins/i18n'
export default {
    components: {
        VMenu
    },
    props: {
        iconSize: {
            type: String,
            default: '1x'
        },
        textSize: {
            type: String,
            default: 'title'
        },
        textColor: {
            type: String,
            default: 'white--text'
        },
        iconColor: {
            type: String,
            default: 'info--text'
        }
    },
    computed: {
        ...mapGetters({
            locale: 'lang/locale',
            locales: 'lang/locales'
        }),
        currentFlag(){
            return 'change this'
        }

    },
    watch: {
        locale(newValue){
            console.log(newValue)
        }
    },
    methods: {
        setLocale (locale) {
            if (this.$i18n.locale !== locale) {
                loadMessages(locale)
                this.$store.dispatch('lang/setLocale', { locale })
            }
        }
    }
}
</script>
