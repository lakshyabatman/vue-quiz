<template>
  <div id="app">
    <div v-if="index==questions.length">
      <p style="color:red">Congratulations, you have finished the quiz</p>
    </div>
    <Header
    :numCorrect="numCorrect"
    :total="total"
    />
    <b-container class="bv-example-row">
  <b-row>
    <b-col sm="6" offset="3">
      <QuestionBox 
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
      />
      </b-col>
   
      </b-row>
    </b-container>
  <Footer/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Footer from './components/Footer.vue'
export default {
  name: 'app',
  components: {
    Header,
    QuestionBox,
    Footer
  },
  data(){
    return{
      questions:[],
      index:0,
      numCorrect:0,
      total:0,
    }
  },
  methods:{
    next: function(){
      if(this.index<this.questions.length){
      this.total++
      }
      this.index++
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++
      }
      this.total++
    }
  },
  mounted:function(){
    fetch("https://opentdb.com/api.php?amount=10&category=27&type=multiple",{
      method:'get'
    })
    .then(response=>{return response.json()})
    .then(jsonData=>{
      this.questions=jsonData.results
    })


  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
