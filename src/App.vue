<script>
import TodoItem from "./components/TodoItem.vue";
import TodoCreator from "./components/TodoCreator.vue";

export default {
  components: {
    TodoCreator
  },
  data() {
    return {
      todos: [],
      isModalVisible: false  // Controls the visibility of the modal
    };
  },
  methods: {
    openModal() {
      this.isModalVisible = true;  // Show the modal when button is clicked
    },
    closeModal() {
      this.isModalVisible = false;  // Hide the modal
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);  // Add the new todo to the list
      this.closeModal();  // Hide the modal after adding the todo
    }
  }
};
</script>

<template>
  <div>
    <TodoItem/>
    <p>Hello, World!</p>
    <button @click="openModal">Add Todo</button>

    <TodoCreator
      :isVisible="isModalVisible"
      @todo-added="addTodo"
      @close="closeModal"
    />

    <ul>
      <li v-for="(todo, index) in todos" :key="index">{{ todo }}</li>
    </ul>
  </div>
</template>

<style scoped>
</style>
