<template>
  <div id="app">
    <div class="container">
      <div class="row">
    <!--<div class="showbottun"></div>
    <HelloWorld msg=""></HelloWorld>
    <HelloWorld msg="Task2"></HelloWorld>-->
    <div class="col-md-6">
    <form class="add_button" v-on:submit.prevent>
        <input type="text" v-model="newItem">
        <button v-on:click="addItem">Add</button>
    </form>
    <div class="button" v-for="(todo,index) in todos" :key="index">
      <button v-on:click="textbox(index)">{{todo.item}}</button>
      <button class="button1" v-on:click.shift="deleteItem(index)">削除</button>
    </div>
    </div>
    <div class="col-md-6">
    <component :is="current"
    v-on:savememo="savememo"
    v-model="msg"
    :todo="todo_show"
    placeholder="メモ"
    name="sample-textarea"
    :number="number"
    :rows="10"
    :cols="50">
    </component>
    </div>
    </div>
    </div>
  </div>
  
  
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import MyTextarea from './components/Textarea.vue'


export default {
  name: 'App',
  components: {
    //HelloWorld,
    MyTextarea
  },
  data:function(){
    return { 
      msg:'',
      newItem:'',
      todos:[],
      current:"MyTextarea",
      //currentView:[],
      number:0,
      todo_show:""
    }
  },
  methods:{
    addItem:function(){
          //alert();
      if(this.newItem ===''){
              return;
      }
      var todo ={
          item: this.newItem,
          msg: ''
          //isDone:false
      };
      //this.current = "MyTextarea";
      //this.currentView.push(this.current);
      //this.todo_show=this.newItem
      console.log("タスクの追加")
      this.todos.push(todo);
      this.newItem='';
    },
    deleteItem:function(index){
        this.todos.splice(index,1)
        //this.currentView.splice(index,1)
    },
    textbox:function(index){
      this.todo_show=this.todos[index].item
      this.number=index;
      console.log(this.number)
      this.msg=this.todos[index].msg;
      console.log("テキストボックス"+this.number+"を表示")
      //console.log(this.msg)
    },
    savememo:function(msg){
      //console.log(number)
      //console.log(this.msg)
      /*if(this.todos[number]===undefined){
        alert("タスクを追加してください")
        return
      }*/
      this.todos[this.number].msg=msg
      //console.log(this.msg)
      //console.log(this.number)
      console.log(this.number+"番目の箱のmsgプロパティは"+this.todos[this.number].msg)
      //this.msg=""
    }
  }}

</script>

<style>

</style>