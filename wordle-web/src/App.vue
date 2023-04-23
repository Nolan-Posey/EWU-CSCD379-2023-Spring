<template>
  <v-app>
    <AppBar></AppBar>
    <main class="pt-16">
      <v-spacer></v-spacer>
      <v-btn @click="setInverseTheme"> Inverse Theme </v-btn>
      <v-btn @click="setDarkTheme"> Dark Theme </v-btn>

      <RouterView />

    </main>
  </v-app>
  
  
</template>

<script setup lang="ts">
import { useTheme } from 'vuetify/lib/framework.mjs'
import AppBar from './components/AppBar.vue'

const theme = useTheme()

function setInverseTheme() {
  theme.global.name.value = 'inverse'
}

function setDarkTheme() {
  theme.global.name.value = 'dark'
}
</script>
