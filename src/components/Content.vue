<template>
   <div class = "container-question">
        <b-jumbotron>
        <template #header></template>

        <template #lead>
      {{ currQuestion.question}}
        </template>

        <hr class="my-4">

        
        <b-list-group>
       
           <b-list-group-item 
              v-for="( option ,index) in shuffledOptions" 
              :key="index"
              @click="selectAnswer(index)"
              :class= "[selectedIndex===index ? 'selected' :'']"
              
              >
                {{option}}
              </b-list-group-item>
       
        </b-list-group>
        

    <b-button 
        variant="primary"
        @click="submitAnswer"
         :disabled="selectedIndex===null"
         >
         Submit
         </b-button>
    <b-button v-on:click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
</div>
</template>

<script>
export default {
    props: {
        currQuestion : Object,
        next: Function,
        increment: Function,
    },
   data() {
       return {
           selectedIndex : null,
           shuffledOptions :[],
           
            }
   },
    computed:{
        options() {
            let options = this.currQuestion.incorrect_answers.slice();
            options.push(this.currQuestion.correct_answer);
           // this.shuffledOptions = options
            return options
        }
    },
    watch:{
        currQuestion(){
            this.selectedIndex = null
            this.shuffleoptions()
        }

    },
   

    mounted:function(){
        this.shuffleoptions()
    },
    methods:{
        selectAnswer(index){
            console.log(index);
           this.selectedIndex = index;
        },
        submitAnswer(){
            let isCorrect = false
            if(this.shuffledOptions[this.selectedIndex]===this.currQuestion.correct_answer)
            {
                isCorrect = true;
            }
            console.log(isCorrect)
           this.increment(isCorrect);
        },
        shuffleoptions (){              // shuffling options
            let options = [...this.currQuestion.incorrect_answers,this.currQuestion.correct_answer]

            var shuffled_array = [...options]

            const lenght = options.length
            const last_index = length -1
            var index = -1;

            while(index<lenght)
            {
                const random_value = index + Math.floor(Math.random() * (last_index-index+1));
                const temp = shuffled_array[random_value];
                shuffled_array[random_value] = shuffled_array[index];
                shuffled_array[index] = temp;
                index++;
            }
            this.shuffledOptions = [...shuffled_array]

        },
        

    }
}
</script>

<style scoped>
.list-group{
    margin-bottom: 16px;
}
.btn{
    margin : 0 6px
}
.list-group-item:hover{
    background: rgb(191, 194, 194);
    cursor: pointer;
} 
.selected{
    background: rgb(105, 190, 211);
}
.correct{
    background : rgb(121, 209, 99)
}
.incorrect{
    background: rgb(209, 103, 103);
}
</style>

