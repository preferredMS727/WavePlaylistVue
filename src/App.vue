<template>
  <v-app id="keep">
    <v-app-bar
      app
      clipped-left
      color="amber lighten-4"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" class="hidden-md-and-up"></v-app-bar-nav-icon>
      <span class="appname ml-3 mr-5 hidden-sm-and-down">{{ $t('appname') }}</span>
      <div class="flex-grow-1"></div>
      <v-img contain v-on:click.native="jumpToLang('/en')" :src="require('@/assets/img/en_flag.png')" class="mr-1" max-height="30" max-width="80"></v-img>
      <v-img contain v-on:click.native="jumpToLang('/hu')" :src="require('@/assets/img/hu_flag.png')" class="mr-1" max-height="30" max-width="80"></v-img>
    </v-app-bar>


    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
      color="grey lighten-4"
    >
      <NavigationDrawer />
    </v-navigation-drawer>

    <v-content>
      <v-container
        class="grey lighten-4 fill-height align-start"
      >

            <v-card
              class="mx-auto"
              width="100%"
            >
              <v-card-text class="mainContent">
                <router-view/>
              </v-card-text>
            </v-card>
            <!-- <WavePlaylist></WavePlaylist> -->

      </v-container>
    </v-content>
  </v-app>
</template>


<script>
import NavigationDrawer from '@/components/NavigationDrawer'
// import WavePlaylist from './components/WavePlaylist'

export default {
  name: 'app',
  props: {
    source: String
  },
  components: {
    NavigationDrawer
    // WavePlaylist
  },
  methods: {
    jumpToLang (langcode) {
      // console.log(langcode)
      window.location.href = langcode
    }
  },
  data: () => ({
    drawer: null,
    search: ''
  })
}
</script>


<style css>
@import url('https://fonts.googleapis.com/css?family=Rubik:300,400,500,700&amp;subsetlatin-ext');
@import url('https://cdn.jsdelivr.net/npm/@mdi/font@3.x/css/materialdesignicons.min.css');

#keep .v-navigation-drawer__border {
  display: none
}

@media screen and (min-width: 600px) {
}

@font-face {
    font-family: 'RhythMus';
    src: url('/static/fonts/rhythmus_kisfej-webfont.woff') format('woff');
    src: url('/static/fonts/rhythmus_kisfej-webfont.ttf') format('truetype');
    font-style:  normal;
    font-weight: normal;
}

span.RhythMus {
    color: black;
    font-family: 'RhythMus';
}

@font-face {
    font-family: 'Gentium_BI';
    src: url('/static/fonts/GenBasBI.woff') format('woff');
    src: url('/static/fonts/GenBasBI.ttf') format('truetype');
    font-style:  italic;
    font-weight: bold;}

.Gentium_BI {
    color: black;
    font-family: 'Gentium_BI';
}

@font-face {
    font-family: 'Gentium_I';
    src: url('/static/fonts/GenBasI.woff') format('woff');
    src: url('/static/fonts/GenBasI.ttf') format('truetype');
    font-style:  italic;
}

.Gentium_I {
    color: black;
    font-family: 'Gentium_I';
}

@font-face {
    font-family: 'Gentium_R';
    src: url('/static/fonts/GenBasR.woff') format('woff');
    src: url('/static/fonts/GenBasR.ttf') format('truetype');
    font-style:  normal;
    font-weight: bold;}

.Gentium_R {
    color: black;
    font-family: 'Gentium_R';
}

.appname {
  font-size: 32px;
  text-shadow: 1px 1px 4px #c0c0c0;
  font-family: 'Gentium_BI';
  color: #000000;
}

h1 {
  font-size: 32px;
  text-shadow: 1px 1px 4px #c0c0c0;
  font-family: 'Gentium_BI';
  color: #000000;
}
.mainContent, .v-dialog {
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -o-user-select: none;
    user-select: none;
}
</style>
