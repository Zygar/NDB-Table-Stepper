<template>
    <main id="App"  class="component" :class="'all-answered-'+allAnswered">
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
            quiz.currentMode = "questions",
            quiz.answeredQuestions = {}, 
            quiz.allAnswered = false
        return quiz
    }, 
    methods: { 
        enterCheckAnswerMode () {
            if (this.allAnswered == true) {
                this.currentMode="answers";    
            }
            else {alert("Please answer all the questions first!")}
        }
     },
    mounted () {
        eventHub.$on('answerCountUpdated', (data) => {
            if (data.answerCount > 0) {
                this.answeredQuestions[data.questionIndex] = true;
            } else if (data.answerCount == 0) {
                this.answeredQuestions[data.questionIndex] = false;
            }
            let qtyAnswers = Object.keys(this.answeredQuestions).length,
                qtyQuestions = this.questions.length;
            if (qtyAnswers == qtyQuestions) {
                console.log("We might be nearing the finish line, one last check")
                for (var o in this.answeredQuestions) {
                    if (this.answeredQuestions[o]) {
                        this.allAnswered = true;
                    }
                    else {this.allAnswered = false}
                } 
            }
        })
    }
}
// and here, when questionsAnswered updates, we run a check—of all the questions, are they all TRUE? if so, quizCompletable is set to true. 
// TODO: 
// Lock answer button until all questions have at least one answer. 
// When mode is "answers", disable input on all checkboxes
// And change "Check Answers" to Reset Answers
// And make Reset answers set everything back to default
</script>

<style type="text/css">
    .all-answered-false button {
        cursor: not-allowed;
        opacity: 0.5;
    }
    .all-answered-true button {
        cursor: pointer;
    }
</style>
