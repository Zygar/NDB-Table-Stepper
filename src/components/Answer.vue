<template>
    <div class="answer" 
        :isRightAnswer="isRightAnswer"
        :answerMode="answerMode"
        :class="'answer-' + answerStatus.answerState">
        <input class="answer-checkbox" type="checkbox" :disabled="answerMode" :id="uuid" v-model="answerStatus.isChecked"> <label class="answer-label" :for="uuid"><span class="label-text">{{answer}}</span></label>
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
            answerMode: Boolean,
            questionIndex: Number
        },
        computed: {
            isRightAnswer () {
                for (var i = this.correctAnswerIndices.length - 1; i >= 0; i--) {
                    let current = this.correctAnswerIndices[i],
                        actual = this.index;
                    if (current == actual) {return true} 
                }
            },
            checkedAnswerDetails() {
                return {
                    isChecked: this.answerStatus.isChecked, 
                    index: this.index,
                    questionIndex: this.questionIndex
                };
            }
        },
        data () {
            let answerStatus = {
                isCorrect: false,
                answerState: "unanswered",
                isChecked: false
            }
            return {answerStatus};
        },
        watch: {
            answerMode () {
                // Triggers on switch to Answer Mode
                if (this.answerMode == true) {
                    console.log("Time to check the answers");
                    if (this.answerStatus.isChecked == true && this.isRightAnswer == true) {
                        this.answerStatus.answerState = "correct";
                        eventHub.$emit('correctAnswer')
                    } else if (this.answerStatus.isChecked != true && this.isRightAnswer == true) {
                        this.answerStatus.answerState = "missed"
                        eventHub.$emit('missedAnswer')
                    } else if (this.answerStatus.isChecked == true && this.isRightAnswer != true) {
                        this.answerStatus.answerState = "incorrect"
                        eventHub.$emit('incorrectAnswer')
                    } else {
                        this.answerStatus.answerState = "irrelevant"
                    }
                } else {
                    console.log("Time to reset...")
                    this.answerStatus.isChecked = false; 
                    this.answerStatus.answerState = "unanswered";
                }
                
            }, 
            checkedAnswerDetails (data) {
                eventHub.$emit('answerChecked', data);
            }
        }
    }
</script>

<style type="text/css">
    .answer-correct {
        /*border: 2px solid green;*/
    }
    .answer-incorrect {
        /*border: 2px solid red;*/
    }
    .answer-missed {
        /*border: 2px solid yellow;*/
    }
</style>
