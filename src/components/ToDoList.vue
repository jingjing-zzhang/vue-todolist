<template>
    <div>
        <h1 v-text="title"></h1>
        <label for="textInput">输入完内容请按“enter”键结束</label>
        <br/>
        <input type="text" id="textInput" v-model="newItem" v-on:keyup.enter="addNew"/>

        <ul>
            <li v-for="item in items"
                v-bind:class="{finished: item.isFinished}"
                v-on:click="toggleFinish(item)">
              {{item.label}}
            </li>
        </ul>
    </div>

</template>

<script>
  import Store from '../store';

export default {
    //name定义组件名称
    name: 'ToDoList',
    /** @ data用来存放数据
     *  当定义一个组件时，data必须声明为返回一个初始数据对象的函数
     * **/
    data () {
        return {
            title: "this is a todolist",
            items: Store.fetch(),
            newItem: ""
        }
    },
    /** @ methods用来存放方法
     *  可以通过vue实例来访问这些方法，方法中的this自动绑定为vue实例
     * **/
    methods: {
        addNew () {
          this.items.push({
              label: this.newItem,
              isFinished: false
          })
          this.newItem = "";
        },
        toggleFinish (item) {
          item.isFinished = !item.isFinished;
        }
    },
    watch: {
        /** @ watch监听vue实例变化
         *    当items值发生变化时保存items到localStorage中
         *    其中 deep: true表示深度监听，可以发现对象内部值得变化
         * **/
        items: {
          handler: function (items) {
              Store.save(items)
          },
          deep: true
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
  font-size:20px;
    cursor: pointer;
}
a {
  color: #42b983;
}
    .finished{
      text-decoration: line-through;
    }
</style>
