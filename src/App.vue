<template>
  <div id="app">
    <div class="container">
    <Header
      v-bind:numCorrect="numCorrect"
      v-bind:numTotal="numTotal"
    />

    <QuestionBox
      v-if="questions.length" 
      v-bind:currentQuestion="questions[index]"
      :next="next"
      :previous="previous"
      :increment="increment"
      :endOfQuiz="endOfQuiz"
      :index="index"
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
      questions:[],
      index:0,
      numCorrect:0,
      numTotal:0,
      endOfQuiz: false
    }
  },
  components: {
    Header, QuestionBox
  },
  methods:{
    next(){
      if (this.index === 9){
        this.endOfQuiz = true
        alert("end of quiz")
      }
      else(this.index++)
      
    },
    previous(){
      this.index--
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++
      }
      this.numTotal++
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
.jumbotron{padding:2rem 1rem;margin-bottom:2rem;background-color:#e9ecef;border-radius:.3rem};
.container{width:100%;padding-right:15px;padding-left:15px;margin-right:auto;margin-left:auto};

.nav-item{margin-bottom:-1px};

.nav-pills .nav-link{border-radius:.25rem};
.nav-pills .nav-link.active,.nav-pills .show>.nav-link{color:#fff;background-color:#007bff};
.nav-fill .nav-item{-webkit-box-flex:1;-ms-flex:1 1 auto;flex:1 1 auto;text-align:center};
.nav-justified .nav-item{-ms-flex-preferred-size:0;flex-basis:0;-webkit-box-flex:1;-ms-flex-positive:1;flex-grow:1;text-align:center};
.btn{display:inline-block;font-weight:400;text-align:center;white-space:nowrap;vertical-align:middle;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;border:1px solid transparent;padding:.375rem .75rem;font-size:1rem;line-height:1.5;border-radius:.25rem;transition:color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out};
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
