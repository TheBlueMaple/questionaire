<template>
  <div id="app">
    <component :is='currentComponent' :questionObj='questionList[1]'></component>
    <control-button></control-button>
  </div>
</template>

<script>
import ControlButton from './components/ControlButton.vue';
import TypeRadio from './components/TypeRadio.vue';
import questionList from './assets/questionList.json';
export default {
  name: 'App',
  data:function(){
    return{
      questionList:questionList,
      answers:[],
      currentComponent:'TypeRadio'
    }
  },
  components: {
    ControlButton,
    TypeRadio
  }
}
</script>

<style>
  *{
    margin:0;
    padding:0;
    list-style-type:none;
  }
  #app{
    width:100vw;
    max-width:1024px;
    height:100vh;
    margin:auto;
    background:linear-gradient(to top,rgb(178, 236, 247),#DDF0ED);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
</style>
