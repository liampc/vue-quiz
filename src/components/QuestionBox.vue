<template>
    <div class="question-box-container">
        <b-jumbotron>
            <template #lead v-if="currentQuestion.question">
                {{currentQuestion.question}}
            </template>

            <hr class="my-4">

            <b-list-group>
                <b-list-group-item v-for="(answer, index) in answers" :key="index" 
                @click.prevent="selectAnswer(index)"
                :class="[selectedIndex === index ? 'selected' :'']">
                    {{answer}}
                </b-list-group-item>
            </b-list-group>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button variant="success" href="#" @click="next">Next Question</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from "lodash"

export default {
    props: {
        currentQuestion: Object,
        next: Function,
    },
    data(){
        return {
            selectedIndex : null,
            shuffledAnswers : [],
        }
    },
    methods: {
        selectAnswer(index){
            this.selectedIndex = index 
        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
        }  
    }, 
    watch: {
        // // #function that will reset the index when question changes and run shuffle function 
        // currentQuestion(){
        //     this.selectedIndex = null 
        //     this.shuffleAnswers()
        // }
        // alternative method is to make an object
        currentQuestion: {
            immediate: true,
            handler(){
                this.selectedIndex = null
                this.shuffleAnswers()
            }
        }

    },
    computed: {
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
    mounted(){
        // to shuffle answer at the start
        this.shuffleAnswers()
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }

    .list-group-item:hover {
        color: white; 
        background-color: lightblue;
        cursor:pointer;
    }

    .selected {
        color:black;
        background-color: lightblue;
    }

    .correct {
        color: black;
        background-color: lightgreen;
    }

    .incorrect {
        color: black;
        background-color: red;
    }
</style>