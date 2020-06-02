<template>
  <div id="app">
    <!-- 通过动态组件来切换题目和最后的答案展示、稍微高一点过渡动画 -->
    <transition>
      <!-- 这里由于使用了组件复用，所以会造成更新数据组件不刷新问题，所以必须加上key -->
      <component ref='questionBox' :key='nowQuestionIndex' :is='currentComponent' :incomingData='incomingData' @changeDisabled='changeDisabled'></component>
    </transition>
    <!-- 控制按钮 -->
    <control-button @handleNext='nextQuestion' @finishQuestionaire='finishQuestionaire' @handleRest='restAnwsers'  :disabled='nextDisabled' :isFinalQuestion='isFinalQuestion'></control-button>
  </div>
</template>

<script>
import ControlButton from './components/ControlButton.vue';
import questionList from './assets/questionList.json';
import TypeRadio from './components/TypeRadio.vue';
import TypeString from './components/TypeString.vue';
import TypeCheckbox from './components/TypeCheckbox.vue';
import TypeText from './components/TypeText.vue';
import ShowAnswers from './components/ShowAnswers.vue';
export default {
  name: 'App',
  data:function(){
    return{
      questionList:questionList,
      answers:[],
      // 当前组件控制
      currentComponent:'',
      // 传入子组件数据控制
      incomingData:null,
      // 现题目索引控制
      nowQuestionIndex:null,
      // 下一题按钮是否不可用
      nextDisabled:false,
      // 是否为最后一题
      isFinalQuestion:false
    }
  },
  mounted:function(){
    // 初始化直接进入答题
    this.nowQuestionIndex = 0;
    this.currentComponent = this.getCurrentComponent();
    this.incomingData = this.questionList[0];
    this.nextDisabled = true;
  },
  methods:{
    // 根据json数据中的type判断题型来决定需要使用什么组件进行渲染
    getCurrentComponent:function(){
      let componentName = null;
      switch(this.questionList[this.nowQuestionIndex].type){
        case 'string':
          componentName = "TypeString";
          break;
        case 'radio':
          componentName = 'TypeRadio';
          break;
        case 'checkbox':
          componentName = 'TypeCheckbox';
          break;
        case 'text':
          componentName = 'TypeText';
          break;
      }
      return componentName;
    },
    // 题目切换、收集上一题答案、判断下一题是否为最后一题、重置传入子组件数据、重置下一题按钮不可用状态
    nextQuestion:function(){
      this.answers.push(this.$refs.questionBox.getAnswer());
      if(++this.nowQuestionIndex == this.questionList.length - 1)
        this.isFinalQuestion = true;
      this.currentComponent = this.getCurrentComponent();
      this.incomingData = this.questionList[this.nowQuestionIndex];
      this.nextDisabled = true;
    },
    // 重置答题，所以控制位全部初始化
    restAnwsers:function(){
      this.nowQuestionIndex = 0;
      this.currentComponent = this.getCurrentComponent();
      this.incomingData = this.questionList[0];
      this.answers = [];
      this.nextDisabled = true;
      this.isFinalQuestion = false;
    },
    // 此方法将由子组件根据用户输入内容来触发、即如果用户没有选择或输入、或为空都不能跳往下一题
    changeDisabled:function(flag){
      this.nextDisabled = flag
    },
    // 完成答卷，使用答案展示组件，传入题目和答案
    finishQuestionaire:function(){
      this.answers.push(this.$refs.questionBox.getAnswer());
      this.currentComponent = 'ShowAnswers';
      this.incomingData = [this.questionList,this.answers];
      this.nextDisabled = true;
    }
  },
  components: {
    ControlButton,
    TypeRadio,
    TypeString,
    TypeCheckbox,
    TypeText,
    ShowAnswers
  }
}
</script>

<style>
  *{
    margin:0;
    padding:0;
    list-style-type:none;
    user-select: none;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
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
    overflow: hidden;
  }
  #app .questionBox{
    width:100%;
    box-sizing: border-box;
    padding:2em;
    overflow: auto;
  }
  .questionBox h1{
    font-size:4vh;
    margin-bottom:1em;
  }
  .v-enter{
    transform: translateY(100vh);
  }
  .v-leave{
    transform: translateY(-100vh);
  }
  .v-enter-active,.v-leave-active{
    opacity: 0.5;
    transition: all 1s;    
  }
</style>
