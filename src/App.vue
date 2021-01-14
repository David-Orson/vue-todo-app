<template>
  <div id="app" class="app">
    <img alt="Vue logo" src="./assets/logo.png" class="logo" />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from "axios";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: "App",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [
        /* 
        {
          id: 1,
          body: "take out the trash",
          completed: false,
        },
        {
          id: 2,
          body: "clean the dishes",
          completed: false,
        },
        {
          id: 3,
          body: "walk the dog",
          completed: false,
        }, */
      ],
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`http://localhost:8081/api/todos/${id}`)
        .then((res) => {
          this.todos = res.data;
        })
        .catch((err) => console.error(err));
    },
    addTodo(newTodo) {
      axios
        .post("http://localhost:8081/api/todos", { id: newTodo.id, body: newTodo.body, completed: false })
        .then((res) => {
          this.todos = res.data;
        })
        .catch((err) => console.error(err));
    },
  },
  created() {
    axios
      .get("http://localhost:8081/api/todos")
      .then((res) => {
        this.todos = res.data;
      })
      .catch((err) => console.error(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-clamp: 1.4;
}

.app {
  display: flex;
  flex-direction: column;
  width: 60%;
  margin: 0 auto;
}

.logo {
  margin: 0 auto;
}

.btn {
  display: inline-block;
  border: none;
  background: #41b883;
  color: #35495e;
  padding: 7px 20px;
  cursor: pointer;
  box-shadow: 1px 1px 4px 0px grey;
}

.btn:hover {
  background: #37a071;
}
</style>
