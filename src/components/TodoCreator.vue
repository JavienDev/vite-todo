<template>
  <div v-if="isVisible" class="overlay" @click.self="closeModal">
    <div class="modal">
      <h2>Add a New Todo</h2>
      <input v-model="newTodo" type="text" placeholder="What do you need to do?" />
      <Button variant="secondary" @click="submitTodo">Add Todo</Button>
      <Button variant="secondary" @click="closeModal">Cancel</Button>
      <ToastNotification
      v-if="isToastVisible"
      :message="toastMessage"
      :type="toastType"
      :duration="3000"
      />
    </div>


  </div>

</template>

<script setup>
import { ref } from 'vue';
import Button from './Button.vue';
import '../style.css';
import ToastNotification from "./ToastNotification.vue";


const isToastVisible = ref(false);
const toastMessage = ref("This is a toast message!");
const toastType = ref("info"); // Default type (info)


const props = defineProps({
  isVisible: {
    type: Boolean,
    required: true,
  }
}); 

const newTodo = ref('');

const emit = defineEmits();

const submitTodo = () => {


  console.log("tracked");
  if (newTodo.value.trim()) {
      if (newTodo.length < 0) {
        toastMessage.value = "Cannot create an empty to-do";
        toastType.value = "error";
        isToastVisible.value = true;
        console.log("is being called");
      return;
    }
    emit('todo-added', newTodo.value);
    console.log("tracked 2");
    showSuccessToast("you have succesfully added a new todo!");
    emit('close');
  }
};

const showSuccessToast = (msg) => {
    toastMessage.value = msg;
    toastType.value = "success";
    isToastVisible.value = true;  
}

const closeModal = () => {
  emit('close');
};

</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  
  align-items: center;
}

.modal {
  background-color: white;
  color: black;
  padding: 20px;
  border-radius: 8px;
  width: 300px;
  text-align: center;
}
button {
  margin-top: 10px;
}
input {
  padding: 10px;
  border-radius: 8px;
}
</style>
