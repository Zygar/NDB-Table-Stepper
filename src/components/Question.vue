<template>
    <div class="question">
        <h2>{{questionText}}</h2>
        <answer v-for="(answer, index) in possibleAnswers" 
                 :index="index" 
                 :answer="answer" 
                 :uuid="questionIndex + '-' + index" 
                 :correctAnswerIndices="correctAnswerIndices"
                 :currentMode="currentMode"></answer>
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';
    import Answer from './Answer.vue';
    export default {
        name: 'Question',
        components: { Answer  },
        props: {
            questionText: String,
            questionIndex: Number,
            correctAnswerIndices: Array,
            possibleAnswers: Array,
            currentMode: String
        }
        // data () {
        // }
    }
</script>

