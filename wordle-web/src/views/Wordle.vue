<template>
  <h1>Wordle Mind Bender</h1>
  <div>
    <v-text-field v-model="guess" label="Guess" variant="solo" @input="getValidGuesses" bg-color="blue-grey-darken-4">
    </v-text-field>

    <v-spacer>
        <v-btn @click="checkGuess" color="light-blue-darken-4">
          Check Answer
        </v-btn>
    </v-spacer>
  
    <v-spacer>
      <v-select v-model="guess" :items="validGuesses" :label="'Valid Guesses: ' + validGuesses.length" bg-color="blue-grey-darken-4" >
        <v-hover></v-hover>
      </v-select>
    </v-spacer>
  
    <v-spacer>
      <h2>{{ guess }}</h2>
      <h3>{{ game.secretWord }}</h3>
    </v-spacer>

    <v-row v-for="word in game.guesses" :key="word.text">
      <v-col v-for="letter in word.letters" :key="letter.char">
        <v-btn :color="letter.Color">
          {{ letter.char }}
        </v-btn>
      </v-col>
    </v-row>
  </div>

  

</template>

<script setup lang="ts">
import { WordleGame } from '@/scripts/wordleGame'
import { WordsService } from '@/scripts/wordsService'
import { ref, reactive } from 'vue'

const guess = ref('')
const game = reactive(new WordleGame())
let validGuesses = WordsService.validWords('')
console.log(game.secretWord)
function checkGuess() {
  game.submitGuess(guess.value)
}
function getValidGuesses() {
  validGuesses = WordsService.validWords(guess.value)
}
</script>