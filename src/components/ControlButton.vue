<template>
    <div class="btn-group">
        <button>重置</button>
        <button :disabled='disabled'>下一题</button>
    </div>
</template>
<script>
export default {
    name:"ControlButton",
    data:function(){
        return{
            disabled:false
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
    }
    .btn-group button{
        font-size:3vh;
        padding:0.5em 2em;
        border-radius: 0.5em;
        border:none;
        margin:10px;
    }
    .btn-group button:first-child{
        background-color:blueviolet;
    }
    .btn-group button:last-child{
        background-color:greenyellow;
    }
</style>