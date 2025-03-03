<script setup>
import Button from './Button.vue';
const props = defineProps({
  todo: {
    type: String,
    required: true,
  },
  index: {
    type: Number,
    required: false,
  }
});

const emit = defineEmits();

const removeTodo = () => {
  emit('remove-todo', props.index);
};
</script>

<template>
  <div class="main-container">
    {{ todo }}
    <Button variant="danger" @click="removeTodo"><span class="buttonText">remove</span></Button>
  </div>
</template>

<style scoped>
.main-container {
  padding: 5px;
  text-align: center;
  color: black;
}
.buttonText {
  color: black;
}
</style>
