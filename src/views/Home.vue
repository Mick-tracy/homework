<template>
  <div id="home">
    <AddTodo @handleAdd="handleAdd" />
    <Todos @handleDelete="handleDelete" :todo="todos" />
  </div>
</template>

<script>
import Todos from '@/components/Todos'

import AddTodo from '@/components/AddTodo'

export default {
  name: 'home',
  data(){
    return{
      todos:[]
    }
  },
  created(){
    // 数据请求   ?_limit=10   只取10条数据
    this.$axios('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => {
      // console.log(res)
      this.todos = res.data;
    })
    .catch(err => {
      console.log(err)
    })
  },
  methods:{
    handleDelete(id){
      // console.log(id)
      this.$axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !== id);
      })
      .catch(err => {
        console.log(err)
      })
    },
    handleAdd(newTodo){
      // es5添加数据
      // this.todos.unshift(newTodo);
      // this.todos.push(newTodo);

      const {title,completed} = newTodo;
      // 上面叫解构，相当于下面两行代码
      // const title = newTodo.title;
      // const completed = newTodo.completed;

      this.$axios.post('https://jsonplaceholder.typicode.com/todos',{
        // 本来应该是title:title  但是名字和值一样的话，es6就直接写一个就可以了
        title,  
        completed
      })
      // es6 添加数据
      // this.todos = [res.data,...this.todos];
      // .then(res => (this.todos = [res.data,...this.todos]))
      .then(res => {
        this.todos = [res.data,...this.todos];
      })
      .catch(err => {
        console.log(err)
      })
    }
  },
  components:{
    Todos,
    AddTodo
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
