<template>
    <div class="questionBox">
        <h1>{{questionObj.question}}</h1>
        <div class="options">
            <p v-for="(option,index) in questionObj.options" :key="index">
                <input :name="questionObj.id" type="radio" :value='option' />{{option}}
            </p>
        </div>
    </div>
</template>
<script>
export default {
    name:'TypeRadio',
    props:['questionObj'],
    data:function(){
        return{
            
        }
    },
    mounted:function(){
        console.log(this.questionObj);
    }
}
</script>
<style scoped>
    .questionBox{
        width:100%;
        box-sizing: border-box;
        padding:2em;
    }
    .questionBox h1{
        font-size:3vh;
        margin-bottom:1em;
    }
    .options>p{
        line-height:2em;
        font-size:3vh;
    }
</style>