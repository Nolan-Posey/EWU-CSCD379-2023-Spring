<template>
      <v-app-bar >

        <v-app-bar-title>The Good Word</v-app-bar-title>
  
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      </v-app-bar>

      <v-navigation-drawer v-model="drawer" app>
        <v-list>
            <v-list-item title="Menu"></v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact">
            <v-list-item>
                <v-btn to="/">Home</v-btn>
            </v-list-item>
                
            <v-list-item>
                <v-btn to="/about">About</v-btn>
            </v-list-item>

            <v-list-item>
                <v-btn to="/wordle">Play Game</v-btn>
            </v-list-item>
        </v-list>
        
      </v-navigation-drawer>
      
  </template>
  
  <script lang="ts">
    export default {
        data: () => ({
            drawer: false,
        }),

        watch: {
            group () {
                this.drawer = false
            }
        }
    }
    
  </script>
  