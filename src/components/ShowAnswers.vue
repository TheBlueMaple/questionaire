<template>
    <div class="answerBox">
        <div class="answerItem" v-for='(oneAnswer,key) in answers' :key="key">
            <h1>{{questionList[key].id}} . {{questionList[key].question}}</h1>
            <p v-if='typeof(oneAnswer) == "object"'>
                <span v-for='(value,key) in oneAnswer' :key="key">{{value}}</span>
            </p>
            <p v-else>{{oneAnswer}}</p>
        </div>
    </div>
</template>
<script>
export default {
    name:'ShowAnswers',
    props:{
        incomingData:{
            type:Array,
            require:true
        }
    },
    mounted:function(){
        this.questionList = this.incomingData[0];
        this.answers = this.incomingData[1];
    },
    data:function(){
        return{
            questionList:[],
            answers:[]
        }
    }
}
</script>
<style scoped>
    .answerBox{
        overflow: auto;
    }
    .answerBox h1{
        font-size:4vh;
        margin-top:1em;
        margin-bottom:1em;
        text-indent: 0.5em;
    }
    .answerItem p{
        text-indent:2em;
    }
    .answerItem p,.answerItem p span{
        font-size:3vh;
    }
    /* 为多结果做格式化处理 */
    .answerItem p span::after{
        content:'、'
    }
    .answerItem p span:last-of-type::after{
        content:''
    }
</style>