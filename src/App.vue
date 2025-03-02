<script setup>
import { ref } from 'vue';
import TodoCreator from './components/TodoCreator.vue';
import TodoItem from './components/TodoItem.vue';

const todos = ref([]);
const isModalVisible = ref(false);

const openModal = () => {
  isModalVisible.value = true;
};

const closeModal = () => {
  isModalVisible.value = false;
};

const addTodo = (newTodo) => {
  todos.value.push(newTodo);
  closeModal();
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};
</script>

<template>
  <div>
    <button @click="openModal">Add Todo</button>

    <TodoCreator
      :isVisible="isModalVisible"
      @todo-added="addTodo"
      @close="closeModal"
    />

    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        :index="index"
        @remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<style scoped>
</style>