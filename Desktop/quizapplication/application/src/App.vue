<template>
  <div class="container">
    <Header 
      :numCorrect="numCorrect"
      :numTotal= "numTotal"
    />
    <QuestionBox 
      v-if="questions.length > 0"
      :currentQuestion = "questions[index]"
      :index= "index"
      :next="next"
      :previous="previous"
      :increment="increment"
      />
  </div>
</template>

<script>
import Header from './components/Header'
import QuestionBox from './components/QuestionBox'
export default {
  name: 'App',
  data(){
    return{
      questions:[],
      index:0,
      numCorrect:0,
      numTotal:0
    }
  },
  components:{
    Header,
    QuestionBox
  },
  methods:{
    next(){
      this.index++
    },
    previous(){
      if(this.index === 0){
        alert('no previous question')
      }else{
        this.index--
      }
    },
    increment(isCorrect){
      if(isCorrect){
          this.numCorrect++
      }
      this.numTotal++
    }
  },
  async mounted(){
     const res =  await fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=hard')
     const respData = await res.json()
     this.questions = respData.results
  }
}
</script>

<style>

</style>
