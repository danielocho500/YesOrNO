<template>
    <img v-if="img" :src="img" alt="bg" />
    <div class="bg-dark"></div>
  
    <div class="indecision-container">
      <input type="text" placeholder="Ask me a Question" v-model="newQuestion"/>
      <p>End the question with a "?" </p>
  
      <div>
        <h2> {{ question }}</h2>
        <p> {{answer}} </p>
      </div>
    </div>
  </template>

<script>
export default {
    name: 'Indecision',
    data() {
        return {
            newQuestion: '',
            question: null,
            answer: 'thinking...',
            img: null,
        }
    },
    methods: {
        async getAnswer(){
            await fetch('https://yesno.wtf/api').then(res => res.json()).then(data => {
                this.img = data.image
                this.answer = data.answer
            })
        }
    },
    watch: {
        newQuestion(newQuestion, oldQuestion) {
            if (newQuestion.endsWith('?')) {
                this.img = null
                this.answer = 'thinking...'
                this.getAnswer()
                this.question = newQuestion
                this.newQuestion = ''
            }
        }
    }
}
</script>

<style scoped>
img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 5px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }
</style>
