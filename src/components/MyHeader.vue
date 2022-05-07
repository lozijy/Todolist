<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keydown.enter="add()" v-model="title"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name:"MyHeader",
  data(){
    return{
      title:""
    }
  },
  methods:{
    //调用父传来的函数，把参数传给父亲
    add(){
        const todoobj={
          id:nanoid(),
          title:this.title,
          done:false,
        }
        this.addTodo(todoobj);
        //清空字符串
        this.title = "";
    }
  },
  props:["addTodo"]
}
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
