<template>
  <div class="textare" style="margin-top: 20px;">
    <h3 class="todoshow">{{todo}}</h3>
    
      <textarea 
          name="todo-description"
          placeholder="メモ"
          :value="value"
          :rows="rows"
          :cols="cols"
          @change="saveMemo">
      </textarea>
  
      
        <ul class="nav justify-content-center bg-light">
          <li class="nav-item">
            <a class="nav-link" v-on:click="addTodo">Add</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" v-on:click.shift="deleteTodoItem">Delete</a>
          </li>
        </ul>
      
        </div>
</template>

<script>
export default {
  name: "MyTextarea",
  props: {
    value: { type: String, required: true },
    todo: { type: String, required: true },
    todo2: { type: Number, required: true },
    rows: { type: Number, required: true },
    cols: { type: Number, required: true },
  },
  methods: {
    saveMemo:function(e){
      this.$emit("save-memo",e.target.value)
    },
    deleteTodoItem:function(){
      this.$emit("delete-todo-item",this.todo2)
    },
    addTodo:function(){
      this.$emit("add-todo")
    }
  }
}
</script>

<style>
.todoshow{color:black}
.nav-link{user-select: none;}
</style>