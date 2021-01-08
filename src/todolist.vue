<template>
<div id="app">
    <h2>Todo list</h2>
    <form v-on:submit.prevent>
        <input type="text" v-model="newItem">
        <button v-on:click="addItem">Add</button>
    </form>
    <ul>
        <li v-for="(todo,index) in todos" :key="index">
            <input type="checkbox" v-model="todo.isDone">
            <span v-bind:class="{done:todo.isDone}">{{todo.item}}</span>
            <button class="button1" v-on:click="deleteItem(index)">Delete</button>
        </li>
    </ul>

    <!--<pre>{{$data}}</pre>-->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'Todo',
  data:function(){
      return {
          newItem:'',
          todos:[]
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
          isDone:false
      };
      this.todos.push(todo);
      this.newItem=''
    },
    deleteItem:function(index){
        this.todos.splice(index,1)
    }
  }
}
</script>
<style>

</style>
