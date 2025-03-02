<template>
  <div v-if="isVisible" class="overlay" @click.self="closeModal">
    <div class="modal">
      <h2>Add a New Todo</h2>
      <input v-model="newTodo" type="text" placeholder="What do you need to do?" />
      <button @click="submitTodo">Add Todo</button>
      <button @click="closeModal">Cancel</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
  isVisible: {
    type: Boolean,
    required: true,
  }
}); 

const newTodo = ref('');

const emit = defineEmits();

const submitTodo = () => {
  if (newTodo.value.trim()) {
    emit('todo-added', newTodo.value);
    emit('close');
  }
};

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
