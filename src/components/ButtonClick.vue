<template>
    <div>
        <h1>{{msg2}}</h1>
        <button v-on:click="buttonClick">点击我触发自定义事件!</button>
    </div>
</template>

<script>
  export default {
      name: "ButtonClick",
      /** @ props用来接收来自父组件的数据
       *    1、组件实例的作用域是孤立的，这意味着在子组件的模板内不能直接饮用父组件的数据
       *  父组件中的数据需要使用props才能下发到子组件中。
       *    2、子组件要显式地用props选项声明从父组件中传来的数据，
       *  声明后的数据可以像data数据一样用在子模板中。
       * **/
      props: ["msg2"],
      data () {
          return {
              msg: "我是来自子组件的数据，看到我表示完成了子组件到父组件的通信"
          }
      },
      methods: {
          /** @ 鼠标点击调用buttonClick事件
           *    在事件内部，使用$emit(eventname)来定义子组件触发的事件
           *    如下：子组件触发名为 child-message的自定义事件，并传递参数。
           * **/
          buttonClick: function () {
              this.$emit("child-message", this.msg);
          }
      }
  }
</script>

<style>

</style>
