<template>
    <h2>{{ getTitle }}</h2>


    <p>Count: {{ count }}</p>
    
    <div>
        <button @click="increment">Increment</button>
        <button @click="decrement">Decrement</button>
        <button @click="reset">Reset</button>
    </div>
 
</template>
<script>
export default {
    props: {
        title: String,
        start: {
            type: Number,
            required: false,
            default: 100,
            validator(value){
                return value > 100
            }
        }
    },
    name: 'Counter',
    data() {
        return {
            count: this.start
        }
    },
    methods:{
        increment(){
            this.count++
        },
        decrement(){
            this.count--
        },
        reset(){
            this.count = 0
        }
    },
    computed: {
        squared() {
            console.log('squared computed') 
            return this.count * this.count
        },
        getTitle(){
            return this.title || 'Counter'
        }
    }
}

</script>

<style scoped>

button{
    background-color: #64BB87;
    border-radius: 5px;
    border: 1px solid white;
    cursor: pointer;
    color: white;
    margin: 0 5px;
    transition: 0.3s ease-in-out;
    padding: 5px 15px;
}

button:hover{
    background-color: #5aa67b;
    transition: 0.3s ease-in-out;
}

</style>