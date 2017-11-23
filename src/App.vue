<template>
  <div id="app">
    <ToDoList/>
    <!--@ 在父组件中使用v-on监听子组件触发的事件
        监听了子组件触发的时间做什么呢？在fromChild事件中定义
        如下：ButtonClick监听子组件触发的child-message事件，
             监听到之后触发fromChild事件，更改data中messageFromChild数据
    -->
    <ButtonClick msg2="父组件向子组件的传递信息"
                 v-on:child-message="fromChild"/>
    <p>The message from Child is: <b>{{messageFromChild}}</b></p>
  </div>
</template>

<script>
  import ToDoList from './components/ToDoList';
  import ButtonClick from './components/ButtonClick';

  export default {
      name: 'app',
      /** @ components注册组件
       *  父组件想要在template中调用子组件，除了需要使用import引入之外
       *  还需要在components中注册才可以。
       * **/
      components: {
          ToDoList,
          ButtonClick
      },
      data () {
          return {
              messageFromChild: ""
          }
      },
      methods: {
          fromChild (msg) {
              this.messageFromChild = msg;
          }
      }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  p{
    color: green;
  }
</style>
