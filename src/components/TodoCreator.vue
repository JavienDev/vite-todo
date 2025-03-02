<script>
export default {
  props: {
    isVisible: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      newTodo: ''
    };
  },
  methods: {
    submitTodo() {
      if (this.newTodo.trim()) {
        this.$emit('todo-added', this.newTodo);
        this.newTodo = '';
      }
    },
    closeModal() {
      this.$emit('close');
    }
  }
}
</script>
<template>
  <div v-if="isVisible" class="overlay" @click.self="closeModal">
    <div class="moda">
      <h2>Add a new Todo</h2>
      <input v-model="newTodo" type="text" placeholder="What do you need to do?"/>
      <button @click="submitTodo">Add todo</button>
      <button @click="closeModal">Nevermind</button>
    </div>
  </div>
</template>
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
  padding: 20px;
  border-radius: 8px;
  width: 300px;
  text-align: center;
}
button {
  margin-top: 10px;
}
</style>
