<template>
    <div class="questionBox">
        <h1>{{question.id}} . {{question.question}}</h1>
        <textarea id="" cols="30" rows="10" v-model="answer"></textarea>
    </div>
</template>
<script>
export default {
    name:'TypeText',
    data:function(){
        return{
            question:{
                question:''
            },
            answer:''
        }
    },
    props:{
        incomingData:{
            type:Object,
            require:true
        }
    },
    mounted:function(){
        this.question = this.incomingData;
    },
    watch:{
        answer:function(newValue,oldValue){
            if(newValue == '' && oldValue != '')
                this.$emit("changeDisabled",true);
            else if(newValue != '' && oldValue == '')
                this.$emit("changeDisabled",false);                
        }
    },
    methods:{
        getAnswer:function(){
            return this.answer;
        }
    }
}
</script>
<style scoped>
    textarea{
        width:90%;
        font-size:3vh;
        line-height:2em;
        background-color:transparent;
        border:1px solid blueviolet;
        border-radius: 1em;
        padding:5%;
        outline: none;
    }
</style>