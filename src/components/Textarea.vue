<template>
<div class="textare">
  <h3 class="todoshow">{{todo}}のメモを表示中</h3>
    <textarea 
    :name="name"
    :value="value"
    :placeholder="placeholder"
    :rows="rows"
    :cols="cols"
    @change="savememo">
    </textarea>
    <!--<button v-on:click="savememo">保存</button>-->
</div>
</template>
<script>
export default {
    name: "MyTextarea",
    /*data:function(){
      return{num:0}
    },*/
  props: {
    value: { type: String, required: true },
    name: { type: String, required: true },
    todo:{type:String,required:true},
    placeholder: { type: String, required: false },
    rows: { type: Number, required: false },
    cols: { type: Number, required: false },
    number: { type:Number,required: false}
  },
  methods: {
    //updateValue: function(e) {
      //this.$emit("input", e.target.value);
    //},
    savememo:function(e){
      this.$emit("input", e.target.value)
      //console.log(this.number)
      //this.$emit('savememo',this.number)
      //console.log(this.number)
    }
  }
}
</script>
<style>
.todoshow{color:white}
</style>