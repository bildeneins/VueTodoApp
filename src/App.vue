<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <form class="add_button" v-on:submit.prevent>
            <input type="text" v-model="newItem">
            <button v-on:click="addTodoItem">Add</button>
          </form>
          <div class="button" v-for="(todo,index) in todos" :key="index">
            <button v-on:click="changeSelectingTodo(index)">{{todo.item}}</button>
            <button class="button1" v-on:click.shift="deleteToDoItem(index)">削除</button>
          </div>
        </div>
        <div class="col-md-6">
          <MyTextarea
              v-on:save-memo="saveMemo"
              v-model="msg"
              :todo="todo_show"
              :rows="10"
              :cols="50">
          </MyTextarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MyTextarea from './components/Textarea.vue'


export default {
  name: 'App',
  components: {
    MyTextarea
  },
  data:function(){
    return { 
      msg:'',
      newItem:'',
      todos:[],
      selectingTodoIndex:0,
      todo_show:""
    }
  },
  methods:{
    addTodoItem:function(){
      if(this.newItem ===''){
        return;
      }
      var todo ={
        item: this.newItem,
        msg: ''
      };
      console.log("タスクの追加")
      this.todos.push(todo);
      this.newItem='';
    },
    deleteTodoItem:function(index){
      this.todos.splice(index,1)
    },
    changeSelectingTodo:function(index){
      this.todo_show=this.todos[index].item
      this.selectingTodoIndex=index;
      console.log(this.selectingTodoIndex)
      this.msg=this.todos[index].msg;
      console.log("テキストボックス"+this.selectingTodoIndex+"を表示")
    },
    saveMemo:function(msg){
      this.todos[this.selectingTodoIndex].msg=msg
      console.log(this.selectingTodoIndex+"番目の箱のmsgプロパティは"+this.todos[this.selectingTodoIndex].msg)
    }
  }
}
</script>

<style>

</style>