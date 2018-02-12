<template>
    <main id="App"  class="component">
       <h1>Welcome</h1>
       <question v-for="(question, index) in questions" 
                 :questionText="question.questionText" 
                 :possibleAnswers="answers" 
                 :correctAnswerIndices="question.correctAnswerIndices" 
                 :questionIndex="index"
                 :currentMode="currentMode"></question>
       <button @click="enterCheckAnswerMode()">Check Answers</button>
    </main>
</template>

<script>
// import sourceData from './content/_data.js';
// import InfoView from './components/InfoView.vue';
// import NavigationView from './components/NavigationView.vue';
import eventHub from './eventHub.js';
import Question from './components/Question.vue';
import data from './content/_data.js';
export default {
    name: 'app', 
    components: { Question  },
    data () { 
        let quiz = data;
            quiz.currentMode = "questions"
        return quiz
    }, 
    methods: { 
        enterCheckAnswerMode () {
            this.currentMode="answers";
        }
     }
}
</script>
