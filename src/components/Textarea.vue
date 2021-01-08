<template>
  <div class="textare">
    <h3 class="todoshow">{{todo}}のメモを表示中</h3>
      <textarea 
          name="todo-description"
          placeholder="メモ"
          :value="value"
          :rows="rows"
          :cols="cols"
          @change="saveMemo">
      </textarea>
  </div>
</template>

<script>
export default {
  name: "MyTextarea",
  props: {
    value: { type: String, required: true },
    todo: { type: String, required: true },
    rows: { type: Number, required: true },
    cols: { type: Number, required: true }
  },
  methods: {
    saveMemo:function(e){
      this.$emit("save-memo",e.target.value)
    }
  }
}
</script>

<style>
.todoshow{color:black}
</style>