<template>
  <div id="app">
   <Header
    :numTots = "numTots"
    :numCorrect = "numCorrect" 
   />
   <b-container class="bv-example-row">
  <b-row>
    <b-col sm ="6" offset="3">  
      <Content
      v-if="questions.length"
        :currQuestion="questions[index]"
        :next="next"
        :increment="increment"
      />
      </b-col>
  </b-row>
</b-container>
 
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Content from './components/Content.vue'

export default {
  name: 'App',
  components: {
    Header,
    Content 
  },
  data(){
    return {
      questions:[],
      index: 0,
      numCorrect :0,
      numTots:0,
    }
  },
  methods:{
    next(){
      this.index++
    },
    increment(isCorrect){
      if(isCorrect)
      {
        this.numCorrect++;
      }
      this.numTots++;
    },
  },
  mounted : function(){
    fetch('https://opentdb.com/api.php?amount=10&type=multiple',
      {method :'get'}
    )
    .then((response) =>{
      return response.json()  
    })
    .then((jsonData)=>{
        this.questions = jsonData.results
    })
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
  

// https://opentdb.com/api.php?amount=10