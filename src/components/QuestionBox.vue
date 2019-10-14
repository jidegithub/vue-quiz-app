<template>
<div>
    <section class="hero is-dark is-small">
        <div class="hero-body">
            <div class="container">
                <h1 class="title">
                    {{ Currentquestion.question }}
                </h1>
            
                <a v-for="(allAnswer, index) in answer" v-bind:key="index" 
                class="navbar-item"
                v-on:click="selectedAnswer(index)"
                v-bind:class="addSelectedClass(index)"
                >
                    {{ allAnswer }}
                </a>
            </div>
        </div>
    </section>
    <div class="field">
        <div class="control">
            <input class="button" type="button" value="submit">
        </div>
        <div class="control">
            <input class="button" v-on:click.enter="nextQuestion"  type="button" value="next">
        </div>
    </div>
</div>
</template>

<script>
export default {
    props:{
        Currentquestion: Object,
        nextQuestion: Function,
    },
    data(){
        return{
            selectedAnswerIndex:null,
            correctAnswerIndex:null,
        }
    },
    methods:{
        selectedAnswer(index){
            this.selectedAnswerIndex = index;
            console.log(this.selectedAnswerIndex, index)
        },
        addSelectedClass(index){
            let addSelectedClass = ''
            this.selectedAnswerIndex === index ? addSelectedClass ='selected' : ''
            return addSelectedClass;
        },
        shuffleAnswer(array){
            for(let i = array.length - 1; i > 0; i--){
                let j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
    },
    computed:{
        answer() {
            let answers = this.Currentquestion.incorrect_answers
            answers.unshift(this.Currentquestion.correct_answer)
            return answers;
        },
        
    },
    watch:{
        Currentquestion(){
            this.selectedAnswerIndex = null;
        }
    },
    mounted(){
        this.shuffleAnswer(this.allAnswersArray)
    }
}
</script>

<style>
    .selected{
        background-color: #292929;
    }
    .correct{
        background-color: aquamarine;
    }
    .incorrect{
        background-color: salmon;
    }
</style>