<template>
    <div class="questionBox">
        <h1>{{question.id}} . {{question.question}}</h1>
        <div class="options">
            <p v-for="(option,index) in question.options" :key="index">
                <input name="labels" type="checkbox" :value='option' v-model='answers' :id="'option'+index" />
                <label :for="'option'+index">{{option}}</label>
            </p>
        </div>
    </div>
</template>
<script>
export default {
    name:'TypeCheckbox',
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
                options:[],
            },
            answers:[]
        }
    },
    mounted:function(){
        this.question = this.incomingData;
    },
    watch:{
        answers:function(newValue,oldValue){
            if(newValue.length == 0  && oldValue.length > 0)
                this.$emit("changeDisabled",true);
            else if(newValue.length > 0  && oldValue.length == 0)
                this.$emit("changeDisabled",false);                
        }
    },
    methods:{
        getAnswer:function(){
            return this.answers;
        }
    }
}
</script>
<style scoped>
    .options>p{
        line-height:3em;
        font-size:3vh;
    }
    .options>p>input{
        display: none;
    }
    .options>p>input[type='checkbox']:checked+label::before{
        background-clip: content-box;
        background-color:rgb(62, 6, 116);
    }
    .options>p>label::before{
        content:'';
        display: inline-block;
        width:2vh;
        height:2vh;
        padding:0.5vh;
        border-radius: 10%;
        border:1px solid blueviolet;
        vertical-align: middle;
        margin-right:1em;
    }
</style>