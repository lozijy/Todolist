<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"/>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
        <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyList from './components/MyList.vue'
import MyFooter from './components/MyFooter.vue'
import MyItem from "@/components/MyItem";

export default {
  name:"App",
  components:{
    // eslint-disable-next-line vue/no-unused-components
  MyList,MyFooter,MyHeader,MyItem
  },
  data(){
    return{
      //存放数据,由additem方法传输数据
      todos:[],
    }
  },
  methods:{
    //添加todo方法,参数由myheader提供
    addTodo(todoobj){
      this.todos.unshift(todoobj);

    },
    //检查给定id的todo的属性done是否为true,返回对应的bool类型
    checkTodo(id){
      this.todos.forEach((todo)=>{
        if(todo.id===id &&todo.done===false)
        {
          todo.done=true
        }else if(todo.id===id &&todo.done===true)todo.done=false;
      })
    },
    deleteTodo(id){
      this.todos=this.todos.filter((todo)=>{
        return todo.id!==id;
      })
    },
    checkAllTodo(){
      this.todos.forEach(todo=>{
        todo.done=true;
      })
    },
    clearAllTodo(){
      this.todos=this.todos.filter(todo=>{
        return todo.done===false;
      })
    }
  }
}
</script>

<style>
body {
  background: #fff;
}
.todo-container {
  width: 600px;
  margin: 50px auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
