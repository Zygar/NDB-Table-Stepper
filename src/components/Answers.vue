<template>
    <div class="answers">
        <div v-for="(answer, index) in possibleAnswers">
            <input type="checkbox" :id="questionIndex + '-' + index"> <label :for="questionIndex + '-' + index">{{answer}}</label>
        </div>
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';

    export default {
        name: 'Answers',
        props: {
            correctAnswerIndices: Array,
            possibleAnswers: Array,
            questionIndex: Number
        }
        // data () {
        // }
    }
</script>

