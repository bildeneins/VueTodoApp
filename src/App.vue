<template>
  <div id="app">
    
    <div class="container">
      <div class="row">
        <div class="col-md-6" style="margin-top: 50px;">
          <div v-for="(todo,index) in todos" :key="index">
            <div v-on:click="changeSelectingTodo(index)" style="text-align: left; padding:10px;" class="button col-md-10 border-bottom rounded-0" v-bind:class="{ 'is-active': activeItem === index }">{{todo.item}}</div>
            </div>
          
        </div>
        <div class="col-md-6">
          <MyTextarea
              v-on:delete-todo-item="deleteTodoItem"
              v-on:add-todo="addTodo"
              v-on:save-memo="saveMemo"
              v-model="msg"
              :todo="todo_show"
              :todo2="todo_show2"
              :rows="15"
              :cols="75">
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
      todo_show:"新規追加",
      todo_show2:null,
      active:false,
      activeItem: null,
      }
    },
  methods:{
    deleteTodoItem:function(){
      this.todos.splice(this.todo_show2,1)
      this.todo_show='';
      this.msg='';
      this.activeItem='';
    },
    changeSelectingTodo:function(index){
      this.todo_show=this.todos[index].item+"のメモを表示中"
      this.todo_show2=index;
      this.selectingTodoIndex=index;
      console.log(this.selectingTodoIndex)
      this.msg=this.todos[index].msg;
      this.active=true;
      console.log("テキストボックス"+this.selectingTodoIndex+"を表示")
      if(this.activeItem === index){
          this.activeItem = null;
        }else{
          this.activeItem = index;
        }
    },
    saveMemo:function(msg){
      console.log('here')
      if(this.todo_show==='新規追加'){
        if(msg==''){
          return;
        }
        var memo=msg.split(/\n/,2);
        var memo2=msg.replace(memo[0],'');
        var memo3=memo2.replace(/\n/,'')
        var todo ={
        item: memo[0],
        msg: memo3
      }
      console.log("タスクの追加")
      this.todos.push(todo);
      this.todo_show='';
      this.msg='';
      }
      else{
        this.todos[this.selectingTodoIndex].msg=msg;
        console.log(this.selectingTodoIndex+"番目の箱のmsgプロパティは"+this.todos[this.selectingTodoIndex].msg)
      }
    },

    addTodo:function(){
      this.todo_show='新規追加';
      this.activeItem='';
      this.msg='';
    }
  }
}
</script>

<style>
  .line {
  margin: 0 1rem;
  width: 4px;
  background-color: #000;
}
.button:hover{
  background-color: rgba(254,220,94,0.2);
}
.is-active {
  background-color: rgba(254,220,94,0.6)!important;
}


</style>