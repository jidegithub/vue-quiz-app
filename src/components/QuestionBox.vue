<template>
<div>
    <div class="jumbotron">
      <p>
       {{ currentQuestion.question }}
      </p>
    </div>
    <hr>
    <p class="answers" v-for="(answer, index) in answers" v-bind:key="index"
    v-on:click="selectAnswer(index)"
    v-bind:class="[ 
        !answered && selectedIndex === index ? 'selected' : 
        answered && correctIndex === index ? 'correct' : 
        answered && selectedIndex === index && correctIndex !== index ? 'incorrect' : ''
    ]"
    >
        {{ answer }}
    </p>
    <button class="btn btn-primary" type="submit"
        v-on:click="submitAnswer"
        v-bind:disabled="selectedIndex === null || answered"
    >
        submit
    </button>
    <button v-on:click="previous" v-bind:disabled="!endOfQuiz && index === 0" class="btn btn-primary" type="submit">previous</button>
    <button v-on:click="next" v-bind:disabled="endOfQuiz" class="btn btn-primary" type="submit">next</button>
</div>
  
</template>

<script>
import _ from 'lodash';
export default {
    props:{
        currentQuestion: Object,
        next:Function,
        increment:Function,
        previous:Function,
        endOfQuiz:Boolean,
        index:Number
    },
    data(){
        return{
            selectedIndex: null,
            correctIndex: null,
            shuffledAnswers: [],
            answered:false
        }
    },
    computed:{
        answers() {
           let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers;
        }
    },
    watch:{
        currentQuestion:{
            immediate: true,
            handler(){
                this.selectedIndex = null
                this.answered = false
                this.shuffleAnswers() 
            }
        }
        // (){
        //     this.selectedIndex = null
        //     this.shuffleAnswers()
        // }
    },
    methods:{
        selectAnswer(index){
            this.selectedIndex = index
        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers);
            this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)

        },
        submitAnswer(){
            let isCorrect = false;

            if(this.selectedIndex === this.correctIndex){
                isCorrect = true;
            }
            this.answered = true
            this.increment(isCorrect)
        }

    },
    // mounted(){
    //     this.shuffleAnswers()
    // }
}
</script>

<style scoped>
    .answers{
        width: 50%;
    }
    .answers:hover{
        background-color:#eee;
        cursor: pointer;
    }
    .selected{
        background-color: lightblue;
    }
    .correct{
        background-color: lightgreen;
    }
    .incorrect{
        background-color: lightsalmon;
    }
</style>