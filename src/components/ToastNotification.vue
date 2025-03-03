<template>
    <div
      v-if="isVisible"
      class="fixed bottom-5 left-1/2 transform -translate-x-1/2 px-4 py-2 rounded shadow-lg transition-opacity duration-300"
      :class="toastClasses"
      @click="closeToast"
      :style="{ transition: `opacity ${duration / 1000}s`, zIndex: 9999 }"
    >
      <slot>{{ message }}</slot> <!-- Default content slot with fallback to message prop -->
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount, computed } from "vue"; // Add computed here
  
  // Define props for the toast message, duration, and type
  const props = defineProps({
    duration: {
      type: Number,
      default: 3000, // Default duration in milliseconds
    },
    message: {
      type: String,
      default: "This is a toast message!",
    },
    type: {
      type: String,
      default: "info", // Default to 'info' type
    },
  });
  
  // Reactive state for toast visibility
  const isVisible = ref(false);
  
  // Show the toast when the component is mounted
  onMounted(() => {
    isVisible.value = true;
    // TODO: remove this fucking code below
    console.log(isVisible.value);
  
    // Hide the toast after the specified duration
    setTimeout(() => {
      isVisible.value = false;
      // TODO: remove this as well
      console.log(isVisible.value);
    }, props.duration);
  });
  
  // Automatically close the toast before unmounting the component
  onBeforeUnmount(() => {
    isVisible.value = false;
  });
  
  // Close the toast when clicked
  const closeToast = () => {
    isVisible.value = false;
  };
  
  // Compute the classes based on the toast type
  const toastClasses = computed(() => {
    switch (props.type) {
      case "success":
        return "bg-green-500 text-white";
      case "error":
        return "bg-red-500 text-white";
      case "warning":
        return "bg-yellow-500 text-white";
      default:
        return "bg-blue-500 text-white";
    }
  });
</script>

  
  <style scoped>
  /* Optional: Add styles for smooth animation, positioning, etc. */
  </style>
  