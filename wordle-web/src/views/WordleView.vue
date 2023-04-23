<template>
  <h1>Wordle Mind Bender</h1>
  
  <GameBoard :game="game" @letterClick="addChar" />

  <v-spacer>
    <v-divider></v-divider>

  </v-spacer>

  <v-text-field
    v-model="guess"
    label="Guess"
    variant="solo"
    @keydown.prevent="($event:KeyboardEvent) => keyPress($event)"
  ></v-text-field>

 <v-select
    v-model="guess"
    :items="validGuesses"
    :label="'Valid Guesses: ' + validGuesses.length"
    bg-color="blue-grey-darken-4"
    >
    <v-hover></v-hover>
  </v-select>

  <KeyBoard @letterClick="addChar" :guessedLetters="game.guessedLetters" />

  <v-btn @click="checkGuess" @keyup.enter="checkGuess"> Check </v-btn>

  <h2>{{ guess }}</h2>
  <h3>{{ game.secretWord }}</h3>

</template>

<script setup lang="ts">
import { WordleGame } from '@/scripts/wordleGame'
import { ref, reactive } from 'vue'
import GameBoard from '../components/GameBoard.vue'
import KeyBoard from '../components/KeyBoard.vue'
import type { Letter } from '@/scripts/letter'
import { watch, onMounted, onUnmounted } from 'vue'
import { WordsService } from '@/scripts/wordsService'
import ValidGuesses from '@/components/ValidGuesses.vue'

let validGuesses = new Array<string>()
let validWord = ''
const guess = ref('')
const game = reactive(new WordleGame())
console.log(game.secretWord)

onMounted(() => {
  window.addEventListener('keyup', keyPress)
})
onUnmounted(() => {
  window.removeEventListener('keyup', keyPress)
})

watch(
  guess,
  (newGuess, oldGuess) => {
    if (newGuess.length > 5) {
      guess.value = oldGuess || ''
    }
  },
  { flush: 'post' }
)

function checkGuess() {
  game.submitGuess()
  guess.value = ''
  getValidGuesses()
}

function addChar(letter: Letter) {
  game.guess.push(letter.char)
  guess.value += letter.char
  getValidGuesses()
}

function keyPress(event: KeyboardEvent) {
  console.log(event.key)
  if (event.key === 'Enter') {
    checkGuess()
  } else if (event.key === 'Backspace') {
    guess.value = guess.value.slice(0, -1)
    console.log(validWord)
    getValidGuesses()
    game.guess.pop()
    console.log('Back')
  } else if (event.key.length === 1 && event.key !== ' ') {
    guess.value += event.key.toLowerCase()
    console.log(validWord)
    getValidGuesses()
    game.guess.push(event.key.toLowerCase())
  }
  //event.preventDefault()
}

function getValidGuesses() {
  validGuesses = WordsService.validWords(guess.value)
}
</script>
