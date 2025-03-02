<script lang="ts">
export default {
    name: "TodoItem",
    props: {
      todo: {
        type: String,
        required: true,
      },
      index: {
        type: Number,
        required: false
      }
    },
    methods: {
      removeTodo() {
        this.$emit('remove-todo', this.index);
      }
    }
}
</script>

<template>
  <div class="main-container">
    {{ todo }}
    <button @click="removeTodo">remove</button>
  </div>
</template>

<style scoped>
.main-container {
  padding: 50px;
  text-align: center;
  color: red;
}

</style>
