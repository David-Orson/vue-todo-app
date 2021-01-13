<template>
  <div class="add-todo">
    <form @submit="addTodo">
      <input type="text" v-model="body" name="body" placeholder="Task..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuid } from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      body: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuid(),
        body: this.body,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
    },
  },
};
</script>

<style scoped>
.add-todo {
  margin: 30px 0px;
}

form {
  display: flex;
}

input[type="text"] {
  border-radius: 4px;
  flex: 8;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 600;
  margin-left: 40px;
}
</style>
