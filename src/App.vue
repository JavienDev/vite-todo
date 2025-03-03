<script setup>
import { ref } from 'vue';
import TodoCreator from './components/TodoCreator.vue';
import TodoItem from './components/TodoItem.vue';
import Button from './components/Button.vue';
import ToastNotification from "./components/ToastNotification.vue";


const isToastVisible = ref(false);
const toastMessage = ref("This is a toast message!");
const toastType = ref("info"); // Default type (info)



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
  showSuccessToast("A new todo has been succesfully added!");
  closeModal();
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};


const showSuccessToast = (msg) => {
    toastMessage.value = msg;
    toastType.value = "success";
    isToastVisible.value = true;  
    setTimeout(() => {
      isToastVisible.value = false;
    }, 3000);
}


</script>

<template>
  <div>
    <div className="bg-red-500 p-4 text-white flex justify-between">Simple To-Do
      <Button variant="secondary" @click="openModal">Add Todo</Button>
    </div>


    <TodoCreator
      :isVisible="isModalVisible"
      @todo-added="addTodo"
      @close="closeModal"
    />

    <ToastNotification
      v-if="isToastVisible"
      :message="toastMessage"
      :type="toastType"
      :duration="3000"
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
