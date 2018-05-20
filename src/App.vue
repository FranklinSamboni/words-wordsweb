<template>
  <v-app>
    <v-toolbar
      app
    >
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn color="Dark" v-on:click.native="update" right="rigth">Actualizar</v-btn>
    </v-toolbar>
    <v-content>
      <router-view ref="router"/>
    </v-content>
    <v-footer  app>
      <span>&copy; 2018</span>
    </v-footer>
  </v-app>
</template>

<script>

import { EventBus } from './components/event-bus.js';

export default {
  data () {
    return {
      rigth: true,
      title: 'Words App'
    }
  },
  name: 'App',
  methods:{
    update(){
      EventBus.$emit('updateWords', null );
    }
  }
}
</script>
