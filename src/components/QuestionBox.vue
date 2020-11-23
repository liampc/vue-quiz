<template>
    <div class="question-box-container">
        <b-jumbotron>
            <template #lead>
                {{currentQuestion.question}}
            </template>

            <hr class="my-4">

            <!-- <p v-for="(answer, index) in answers" :key="index">
                {{answer}}
            </p> -->
            <b-list-group>
                <b-list-group-item v-for="(answer, index) in answers" :key="index">
                    {{answer}}
                </b-list-group-item>
            </b-list-group>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button variant="success" href="#" @click="next">Next Question</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: {
        currentQuestion: Object,
        next: Function,
    },
    computed: {
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }
</style>