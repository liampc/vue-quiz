<template>
  <div id="app">
    <Header />
    <b-row>
      <b-col sm="6" offset="3">
        <QuestionBox :currentQuestion="question[index]"/>
      </b-col>
    </b-row> 
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
  },
  data(){
    return {
      question: [],
      index: 0
    }
  },    
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=31&difficulty=easy&type=multiple', {
      method: 'GET',
    })
    .then((response) => response.json())
    .then((jsonData) => this.question = jsonData.results)
  }
} 
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
