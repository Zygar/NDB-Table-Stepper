<template>
    <div class="answer">
        <input type="checkbox" :id="uuid"> <label :for="uuid">{{answer}}</label>
    </div>
</template>

<script>
    import eventHub from '../eventHub.js';

    export default {
        name: 'Answers',
        props: {
            answer: String,
            index: Number,
            uuid: String
        },
        // computed: {
        //     isCorrect () {
        //         for (var i = this.correctAnswerIndices.length - 1; i >= 0; i--) {
        //             let current = this.correctAnswerIndices[i],
        //                 actual = this.index;

        //             if (current == actual) {console.log(current, actual); return true}
        //         }
        //     }
        // }
        // data () {
        // }
    }
</script>

