<template>
    <div class="btn-group">
        <button @click='$emit("handleRest")'>重置</button>
        <button :disabled='disabled' @click='handleNext'>{{ isFinalQuestion ? "完成问卷" : "下一题"}}</button>
    </div>
</template>
<script>
export default {
    name:"ControlButton",
    props:{
        disabled:{
            type:Boolean,
            require:true
        },
        isFinalQuestion:{
            type:Boolean,
            require:true
        }
    },
    data:function(){
        return{
        }
    },
    methods:{
        handleNext:function(){
            if(this.isFinalQuestion)
                this.$emit("finishQuestionaire");
            else
                this.$emit("handleNext");
        }
    }
}
</script>
<style scoped>
    .btn-group{
        width:100%;
        display: flex;
        justify-content: space-evenly;
        margin-bottom:10px;
        margin-top:10px;
    }
    .btn-group button{
        font-size:3vh;
        padding:0.5em 2em;
        border-radius: 0.5em;
        border:none;
        margin:10px;
        outline: none;
    }
    .btn-group button:first-child{
        background-color:blueviolet;
    }
    .btn-group button:last-child{
        background-color:greenyellow;
    }
</style>