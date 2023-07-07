<script setup lang="ts">
import Todo from "../models/Todo.js";
import { ref } from "vue";

const todos = ref<Todo[]>([]);
const userInput = ref("");

//lägg till todo
const addTodo = () => {
  if (userInput.value.trim() !== "") {
    todos.value.push(new Todo(userInput.value, false));

    userInput.value = "";
  }
};

//ta bort todo

const removeTodo = (todo: Todo) => {
  const index = todos.value.indexOf(todo);
  console.log(index);
};
</script>

<!-- använd inte .value i template då vue kommer att ha det värdet automatiskt. bara state.text räcker -->
<template>
  <div class="wrapper">
    <input v-model="userInput" placeholder="Vad behöver göras?" type="text" />
    <button @click="addTodo">Lägg till</button>
  </div>
  <div v-for="todo in todos" :key="todo.text">
    {{ todo.text }}
    <button>ta bort</button>
  </div>
</template>

<style scoped lang="css">
.wrapper {
  display: flex;
  gap: 1rem;
}
button {
  background-color: rgb(194, 192, 192);
}

input {
  text-align: center;
  width: 20rem;
}
</style>
