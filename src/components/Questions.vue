<template>
    <div>
        <div class="questions-ctr">
            <div class="progress">
                <div class="bar" :style="{ width: `${(questionAnswered / questions.length) * 100}%` }"></div>
                <div class="status">{{ questionAnswered }} out of {{ questions.length }} questions answered</div>
            </div>
            <div class="single-question" v-for="(question, qi) in questions" :key="question.q"
                v-show="questionAnswered === qi">
                <div class="question">{{ question.q }}</div>
                <div class="answers">
                    <div class="answer" v-for="answer in question.answers" :key="answer.text"
                        @click="selectAnswer(answer.is_correct)">
                        {{ answer.text }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Questions',
    props: ["questions", "questionAnswered"],
    emits: ["question-answered"],
    methods: {
        selectAnswer(is_correct) {
            this.$emit("question-answered", is_correct)
        }
    },

}
</script>