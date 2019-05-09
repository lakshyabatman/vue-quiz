<template>
<div class="question-box-container">
  <b-jumbotron>

    <template slot="lead">
      {{currentQuestion.question}}
    </template>

    <hr class="my-4">

    <b-list-group>
    
            <b-list-group-item v-for="(answer,index) in answers"  :key="index" @click.prevent="selectAnswer(index)"  :class="[answerClass(index)]">{{answer}}</b-list-group-item>
    </b-list-group>
    <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex===null || answered===true" class="mr-2" href="#">Submit</b-button>
    <b-button variant="success" @click="next" href="#">Next </b-button>
  </b-jumbotron>
</div>
</template>
<script>
import _ from 'lodash'
export default {
    props:{
        currentQuestion:Object,
        next:Function,
        increment:Function
    },
    data(){
      return {
        selectedIndex:null,
        correctIndex:null,
        answered:false,
      }
    },
    watch:{
      currentQuestion(){
         this.selectedIndex=null
         this.answered=false
      }
    },
    methods:{
      selectAnswer(index){
      this.selectedIndex=index
      },
      answerClass(index){
      let answerClass=''
      if(!this.answered && this.selectedIndex===index){
        answerClass='selected'
      }else if(this.answered && this.correctIndex===index){
        answerClass='correct'
      }else if(this.answered && this.selectedIndex===index && this.correctIndex!==index){
        answerClass='incorrect'
      }
      return answerClass
      },
      submitAnswer(){
        this.correctIndex=this.answers.indexOf(this.currentQuestion.correct_answer)
        let isCorrect=false;
        this.answered=true
        if(this.selectedIndex===this.correctIndex){
          isCorrect=true
        }
        this.increment(isCorrect)
      }
    },
    computed:{
        answers(){
            let answers=[...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            answers=_.shuffle(answers)
            // this.correctIndex=answers.indexOf(this.currentQuestion.correct_answer)
            return answers
        }
    }
}
</script>

<style scoped>
.list-group{
  margin-bottom: 5px;
}
 .list-group-item:hover{
   background-color: #EEE;
   cursor: pointer;
 }
.selected{
  background-color:lightblue;
}
.correct{
  background-color: lightgreen;
}
.incorrect{
  background-color: red;
}

</style>
