<template>
    <div class="question">
        <h2>{{questionText}}</h2>
        <answer v-for="(answer, index) in possibleAnswers" 
                 :index="index" 
                 :answer="answer" 
                 :uuid="questionIndex + '-' + index" 
                 :correctAnswerIndices="correctAnswerIndices"
                 :currentMode="currentMode"
                 :questionIndex="questionIndex"
                 ></answer>
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';
    import Answer from './Answer.vue';
    export default {
        name: 'Question',
        components: { Answer },
        props: {
            questionText: String,
            questionIndex: Number,
            correctAnswerIndices: Array,
            possibleAnswers: Array,
            currentMode: String
        },
        data () {
            let model = {
                answerCount: 0
            }; 
            return model
        },
        mounted() {
            eventHub.$on('answerChecked', (data) => {
                if(data.questionIndex == this.questionIndex && data.isChecked == true){
                    this.answerCount ++
                } else if (data.questionIndex == this.questionIndex && data.isChecked == false) {
                    this.answerCount --
                }
            })
        },
        watch: {
            answerCount() {
                let payload = {
                    questionIndex: this.questionIndex,
                    answerCount: this.answerCount
                }
                eventHub.$emit('answerCountUpdated', payload);
            }
        }
        // data () {
        // }
        // data: hasAtLeastOneAnswer true/false. 
        // this holds an array of the selected answers. when they change, we emit an event to App, simply returning the questionID and true or false depending on whether or not the array is empty or not
    }
</script>

