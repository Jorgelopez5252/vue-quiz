<script setup>
import { ref, computed } from 'vue'

const questions = ref([
	{
		question: 'What does Michael pretend to fire Pam over in season one?',
		answer: 2,
		options: [
			'Dating Jim',
			'Messing with Dwight to much',
			'Stealing post-it Notes',
			'Disrespecting Prison Mike'
		],
		selected: null
	},
	{
		question: 'Whats the companys annual award ceremony called?',
		answer: 1,
		options: [
			'Scotts Tots',
			'The Dundies',
			'Mifflin Majority',
			'Scranton Squad'
		],
		selected: null
	},
	{
		question: 'Who are the 3 main members of the Party Planning Committee?',
		answer: 3,
		options: [
			'Michael, Pam, and Angela',
			'Kelly, Angela and Pam',
			'Ryan , Oscar, and Stanley',
			'Pam, Angela, and Phylis'
		],
		selected: null
	},
	{
		question: 'Why does Andy call Jim “Big Tuna”?',
		answer: 3,
		options: [
			'False, this is not true',
			'Jim told Andy he loves Tuna Sammies',
			'Andy is just a jerk like that',
			'He saw Jim eating a tuna fish sandwich on his first day at the new branch'
		],
		selected: null
	},
	{
		question: 'What is Dwights favorite TV Show',
		answer: 2,
		options: [
			'Bears',
			'Beats',
			'Battlestar Galactica',
		],
		selected: null
	},
	{
		question: 'Which of Angelas cats did Dwight kill?',
		answer: 0,
		options: [
			'Sprinkles',
			'Bandit',
			'Cookie',
			'Beet'
		],
		selected: null
	},
	{
		question: 'What was the name of Jan Levinsons assistant',
		answer: 1,
		options: [
			'Tyler',
			'Hunter',
			'Jesse',
			'Jacob'
		],
		selected: null
	},
	{
		question: 'Ryan caused the fire at the office warming up what?',
		answer: 3,
		options: [
			'Hot Cocoa',
			'Coffee',
			'Bean Burrito',
			'A Cheese Pita'
		],
		selected: null
	},
	{
		question: 'What was the name of Andys a cappella group at Cornell?',
		answer: 2,
		options: [
			'Big Tunas',
			'The Hey-ohs',
			'Here comes Treble',
			'Cornell Captains'
		],
		selected: null
	},
	{
		question: 'Pam and Jims first kiss took place where?',
		answer: 1,
		options: [
			'Outside the Office after Casino Night',
			'Chilis',
			'Poor Richards',
			'In the Warehouse'
		],
		selected: null
	}
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
const score = computed(() => {
	let value = 0
	questions.value.map(q => {
		if (q.selected != null && q.answer == q.selected) {
			console.log('correct');
			value++
		}
	})
	return value
})

const getCurrentQuestion = computed(() => {
	let question = questions.value[currentQuestion.value]
	question.index = currentQuestion.value
	return question
})

const SetAnswer = (e) => {
	questions.value[currentQuestion.value].selected = e.target.value
	e.target.value = null
}

const NextQuestion = () => {
	if (currentQuestion.value < questions.value.length - 1) {
		currentQuestion.value++
		return
	}

	quizCompleted.value = true
}

</script>

<template>
	<main class="app">
		<div>
			<img src="https://github.com/Jorgelopez5252/vue-quiz/blob/main/images/officeTriviaLogo.jpeg?raw=true"
				id="logoOffice" alt="Office Logo" />
		</div>

		<section class="quiz" v-if="!quizCompleted">
			<div class="quiz-info">
				<span class="question">{{ getCurrentQuestion.question }}</span>
				<span class="score">Score {{ score }}/{{ questions.length }}</span>
			</div>

			<div class="options">
				<label v-for="(option, index) in getCurrentQuestion.options" :for="'option' + index" :class="`option ${getCurrentQuestion.selected == index
					? index == getCurrentQuestion.answer
						? 'correct'
						: 'wrong'
					: ''
				} ${getCurrentQuestion.selected != null &&
					index != getCurrentQuestion.selected
					? 'disabled'
					: ''
				}`">
					<input type="radio" :id="'option' + index" :name="getCurrentQuestion.index" :value="index"
						v-model="getCurrentQuestion.selected" :disabled="getCurrentQuestion.selected"
						@change="SetAnswer" />
					<span>{{ option }}</span>
				</label>
			</div>

			<button @click="NextQuestion" :disabled="!getCurrentQuestion.selected">
				{{
					getCurrentQuestion.index == questions.length - 1
						? 'Finish'
						: getCurrentQuestion.selected == null
							? 'Select an option'
							: 'Next question'
				}}
			</button>
		</section>

		<section v-else>
			<h2>You have finished the quiz!</h2>
			<p>Your score is {{ score }}/{{ questions.length }}</p>
			<div>
				<br>
				<div id="winLoseScreen" >
					<h1>Congrats, on geting through but how did you do?</h1>
					<img src="https://media.tenor.com/X15e67QrANUAAAAC/the-office.gif" id="logoOffice"
						alt="Office Logo" />
				</div>
			</div>
		</section>
	</main>
</template>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Courier New', Courier, monospace;
	/* font-family: The Office; */
}

#logoOffice {
	max-width: 100%;
	width: 640px;
	margin: auto;
	height: auto;
}

#winLoseScreen {
	text-align: center;
}

body {
	background-color: #271c36;
	color: #FFF;
}

.app {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 2rem;
	height: 100vh;
}

h1 {
	font-size: 2rem;
	margin-bottom: 2rem;
}

.quiz {
	background-color: #382a4b;
	padding: 1rem;
	width: 100%;
	max-width: 640px;
}

.quiz-info {
	display: flex;
	justify-content: space-between;
	margin-bottom: 1rem;
}

.quiz-info .question {
	color: #fff;
	font-size: 1rem;
}

.quiz-info.score {
	color: #FFF;
	font-size: 1.25rem;
}

.options {
	margin-bottom: 1rem;
}

.option {
	padding: 1rem;
	display: block;
	background-color: #271c36;
	margin-bottom: 0.5rem;
	border-radius: 0.5rem;
	cursor: pointer;
}

.option:hover {
	background-color: #2d213f;
}

.option.correct {
	background-color: #2cce7d;
}

.option.wrong {
	background-color: #ff5a5f;
}

.option:last-of-type {
	margin-bottom: 0;
}

.option.disabled {
	opacity: 0.5;
}

.option input {
	display: none;
}

button {
	appearance: none;
	outline: none;
	border: none;
	cursor: pointer;
	padding: 0.5rem 1rem;
	background-color: #2cce7d;
	color: #2d213f;
	font-weight: 700;
	text-transform: uppercase;
	font-size: 1.2rem;
	border-radius: 0.5rem;
}

button:disabled {
	opacity: 0.5;
}

h2 {
	font-size: 2rem;
	margin-bottom: 2rem;
	text-align: center;
}

p {
	color: #8F8F8F;
	font-size: 1.5rem;
	text-align: center;
}
</style>