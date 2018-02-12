<template>
    <div class="answer" 
        :isRightAnswer="isRightAnswer"
        :currentMode="currentMode"
        :class="'answer-' + answerStatus.answerState">
        <input type="checkbox" :id="uuid" v-model="answerStatus.isChecked"> <label :for="uuid">{{answer}}</label>
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';

    export default {
        name: 'Answer',
        props: {
            answer: String,
            index: Number,
            uuid: String,
            correctAnswerIndices: Array,
            currentMode: String
        },
        computed: {
            isRightAnswer () {
                for (var i = this.correctAnswerIndices.length - 1; i >= 0; i--) {
                    let current = this.correctAnswerIndices[i],
                        actual = this.index;
                    if (current == actual) {return true} 
                }
            }
        },
        data () {
            let answerStatus = {
                isCorrect: false,
                answerState: "unanswered"
            }
            return {answerStatus};
        },
        watch: {
            currentMode () {
                // Triggers on switch to Answer Mode

                console.log("Time to check the answers");
                if (this.answerStatus.isChecked == true && this.isRightAnswer == true) {
                    this.answerStatus.answerState = "correct";
                } else if (this.answerStatus.isChecked != true && this.isRightAnswer == true) {
                    this.answerStatus.answerState = "missed"
                } else if (this.answerStatus.isChecked == true && this.isRightAnswer != true) {
                    this.answerStatus.answerState = "incorrect"
                } else {
                    this.answerStatus.answerState = "irrelevant"
                }
            }
        }
        // data () {
        // }
        // So we're going to have some data on an Answer to indicate whether it's checked or not.
        // There'll be a method higher up the chain, that upon being fired will trigger a method here
        // And will check whether or not the item is both checked and correct
        // If it's checked and correct we'll set the class to green
        // If it's checked and incorrect we'll set the class to red
        // If it's not checked, and it's the correct answer, we'll set it to yellow
        // We'll then figure out how to bubble something back up to the parent question / app so you can get a total
        // If it's checked and 
    }
</script>

<style type="text/css">
    .answer-correct {
        border: 2px solid green;
    }
    .answer-incorrect {
        border: 2px solid red;
    }
    .answer-missed {
        border: 2px solid yellow;
    }
</style>
