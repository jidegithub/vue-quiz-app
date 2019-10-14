<template>
  <div id="app">
    <div class="container">
      <Header
      v-bind:Currentquestion ="questionIndex"
      />
      <QuestionBox
      v-if="questions.length"
      v-bind:Currentquestion ="questions[questionIndex]"
      v-bind:nextQuestion ="nextQuestion"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import QuestionBox from "./components/QuestionBox";
import axios from "axios";


export default {
  name: 'app',
  data(){
    return{
      questions: [],
      questionIndex:0,
    }
  },
  components: {
    Header, QuestionBox
  },
  methods:{
    nextQuestion(){
      this.questionIndex++
    }
  },
  mounted:function(){
    axios.get('http://localhost:3000/users')
    .then((res)=>{
      this.questions = res.data.results
    })
  }
}
</script>






<style>


</style>
