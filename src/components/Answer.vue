<template>
    <div class="answer" 
        :isCorrect="isCorrect"
        :currentMode="currentMode">
        <input type="checkbox" :id="uuid"> <label :for="uuid">{{answer}}</label>
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
            isCorrect () {
                for (var i = this.correctAnswerIndices.length - 1; i >= 0; i--) {
                    let current = this.correctAnswerIndices[i],
                        actual = this.index;
                    if (current == actual) {return true}
                }
            }
        },
        watch: {
            currentMode () {
                console.log("Time to check the answers")
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

