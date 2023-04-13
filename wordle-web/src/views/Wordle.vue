<template>
  <h1>The Good Word</h1>

  <v-text-field v-model="guess" label="Guess" varient="solo"></v-text-field>
  <v-btn @click="checkGuess1">Check</v-btn>

  <div>
    <v-row v-for="word in guesses">
      <v-col v-for="letter in word" :key="letter.letter">
         <v-card :color="letter.Color">
            <v-card-title>{{ letter.letter }}</v-card-title>
         </v-card>
      </v-col>
    </v-row>
  </div>

  <h2>{{ guess }}</h2>

  <h3>{{ secretWord }}</h3>
</template>

<script setup lang="ts">
import { Letter } from '@/scripts/letter';
import { LetterStatus } from '@/scripts/letter';
import { ref, reactive } from 'vue'


  const guess = ref('')
  const wordList = ['apple', 'begin', 'grape', 'peach', 'crypt', 'zesty', 'color', 'piano', 'jelly', 'juice', 'mazda']
  const secretWord = wordList[Math.floor(Math.random() * wordList.length)]
  const guesses = reactive(new Array<Array<Letter>>())
  console.log(secretWord)

  const checkGuess1 = () => {
    console.log(guess.value)

    // check length of guess (not > 5)
    if(guess.value.length !== secretWord.length) {
      console.log('invalid guess length')
      guess.value = ''
      return
    }

    // check for valid letters using letter list
      // Make list of letter objects for each 26 letters
      // Change Letter.LetterStatus of letters depending on correctness

    const result = new Array<Letter>()
    const guessChars = guess.value.split('')
    const secretChars = secretWord.split('')
    let isCorrect = true
    for(let i = 0; i < 5; i++){
      result.push(new Letter(guess.value[i]))
      if(guess.value[i] === secretWord[i]){
        result[i].status = LetterStatus.Correct
        guessChars[i] = '_'
        secretChars[i] = '_'
        console.log(`Letter ${guess.value[i]} is correct.`)
      } else if(secretWord.includes(guess.value[i])){
        isCorrect = false;
        result[i].status = LetterStatus.Misplaced
        console.log(`Letter ${guess.value[i]} is correct but in wrong location.`)
      }else {
        isCorrect = false
        result[i].status = LetterStatus.Wrong
        console.log(`Letter ${guess.value[i]} is wrong.`)
      }
    }

    for(let i = 0; i < 5; i++){
      if(guessChars[i] !== '_'){
        for(let j = 0; j < 5; j++){
          if(secretChars[j] === guessChars[i]){
           result[i].status = LetterStatus.Misplaced
            guessChars[i] = '_'
            secretChars[i] = '_'
            console.log(`Letter ${i} is misplaced`)
           break
          }
        }
      }
      
    }

    console.log(guessChars)
    console.log(secretChars)
    console.log(result)
    console.log(isCorrect)
    guesses.push(result)
    console.log(guesses)
  }

  

  function checkGuess2() {
    console.log(guess.value)
  }

// 1. initialize the secret word
// 2. 
</script>
