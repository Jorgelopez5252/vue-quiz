<script setup>
import {ref, computed} from "vue"

// question block
const questions= ref([
  {
    question:'What is Vue JS?',
    answer:0,
    options:[
      'A front-end framwork',
      'A library',
      'An ice cream maker'
    ],
    selected:null
  },
  {
    question:'What is vuex?',
    answer:2,
    options:[
      'Vue with an x',
      'A library',
      'Stage Management Library'
    ],
    selected:null
  },
  {
    question:'What is Vue Router used for?',
    answer:1,
    options:[
      'Walking in space',
      'Routing Library for Vue JS',
      'A console tool option'
    ],
    selected:null
  }
  
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score =computed(() => {
  let value = 0
  questions.value.map(a => {
    if(questions.selected == questions.answer) {
      value ++
    }
  })
  return value
})

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

const setAnswer = evt => {
  questions.value[currentQuestion.value].selected = evt.target.value
}

</script>

<template>
 <h1>Hello world</h1>
</template>

<style>
* {
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: 600;
}

body {
  background-color: #271c36;
  color:#fff;
}
</style>
