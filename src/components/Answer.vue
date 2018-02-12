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
            currentMode: String,
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
            }, 
            checkedAnswerDetails (data) {
                console.log("Emitting once")
                eventHub.$emit('answerChecked', data);
            }
        }
        // data () {
        // }
        // upon isChecked change to TRUE, emit an event carrying the index. Question will watch and maintain an array. 
        // upon isChecked change to FALSE, emit an event carrying the index. Question will splice it out of the array. 

        // TODO: Bubble something up to the parents for scoring. 

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
