<template>
    <div class="questionBox">
        <h1>{{question.id}} . {{question.question}}</h1>
        <input type="text" v-model='answer' :placeholder='question.placeholder || "请在此输入"'>
    </div>
</template>
<script>
export default {
    name:'TypeString',
    props:{
        incomingData:{
            type:Object,
            require:true
        }
    },
    data:function(){
        return{
            question:{
                question:'',
                placeholder:''
            },
            answer:'',
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
    .questionBox input{
        line-height:2em;
        font-size:3vh;
        border:none;
        border-bottom:blueviolet 1px solid;
        background-color:transparent;
        outline: none;
    }
</style>