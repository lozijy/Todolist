<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
            <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name:"MyHeader",
  data(){
    return{
      isAll:false

    }
  },
  computed:{
    total(){
      return  this.todos.length;
    },

    doneTotal(){
      return  this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
    }

  },
  methods:{
    clearAll(){
      this.clearAllTodo();
    }
  },
  watch:{
    isAll(newValue){
      // eslint-disable-next-line vue/no-mutating-props
      this.todos.forEach(todo=>{
        todo.done=newValue;
      })
      console.log("isAll改变了")
    }
  },
  props:["todos","checkAllTodo","clearAllTodo"]
}

</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
