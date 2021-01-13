<template>
  <div class="todo-item">
    <input type="checkbox" v-on:change="markComplete" />
    <p v-bind:class="{ 'is-complete': todo.completed }">
      {{ todo.body }}
    </p>
    <button @click="$emit('del-todo', todo.id)" class="del">x</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scope>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: white;
  padding: 10px;
  border: 1px #ccc solid;
  box-shadow: 1px 1px 4px 0px grey;
  border-radius: 4px;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #35495e;
  color: #ff0000;
  border: none;
  padding: 4px 9px 6px 11px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
}
</style>
