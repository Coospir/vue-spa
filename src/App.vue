<template>
  <div id="app">
    <h1>ToDo</h1>
    <AddTodo @add-todo="addToDo"/>
    <TodoList v-bind:list="list" @removeItem="removeItem"/>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
export default {
  name: 'App',
  data() {
    return {
      list: [
        {
          id: 1,
          title: 'Clean the room',
          completed: false
        },
        {
          id: 2,
          title: 'Wash the dishes',
          completed: false
        },
        {
          id: 3,
          title: 'Buy a milk',
          completed: false
        }
      ]
    }
  },
  components: {
    TodoList,
    AddTodo
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json => {
          this.list = json
        })
  },
  methods: {
    removeItem(id) {
      this.list = this.list.filter(l => l.id !== id)
    },
    addToDo(todo) {
      this.list.push(todo)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
