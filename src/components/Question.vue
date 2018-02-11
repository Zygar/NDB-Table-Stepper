<template>
    <div class="question">
        <h2>{{questionText}}</h2>
        <answers v-for="(answer, index) in possibleAnswers" :index="index" :answer="answer" :uuid="questionIndex + '-' + index" ></answers>
        <!-- 
        <answers :correctAnswerIndices="correctAnswerIndices" :possibleAnswers="possibleAnswers" :questionIndex="questionIndex"></answers> -->
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';
    import Answers from './Answers.vue';
    export default {
        name: 'Question',
        components: { Answers  },
        props: {
            questionText: String,
            questionIndex: Number,
            correctAnswerIndices: Array,
            possibleAnswers: Array
        }
        // data () {
        // }
    }
</script>

