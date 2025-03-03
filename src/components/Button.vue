<template>
    <button
      :class="[baseClasses, variantClasses[variant], sizeClasses[size]]"
      :disabled="disabled"
      class="disabled:opacity-50 disabled:cursor-not-allowed"
    >
      <slot />
    </button>
  </template>
  
  <script setup>
  import { computed } from "vue";
  
  // Define props
  const props = defineProps({
    variant: {
      type: String,
      default: "default", // Default variant
      validator(value) {
        return ["default", "secondary", "danger"].includes(value);
      },
    },
    size: {
      type: String,
      default: "md", // Default size
      validator(value) {
        return ["sm", "md", "lg"].includes(value);
      },
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  });
  
  // Computed properties for classes
  const baseClasses = "px-4 py-2 rounded font-medium transition-colors ml-5";
  
  const variantClasses = computed(() => ({
    default: "bg-blue-500 text-white hover:bg-blue-600",
    secondary: "bg-gray-500 text-white hover:bg-gray-600",
    danger: "bg-red-600 text-white hover:bg-red-500",
  }));
  
  const sizeClasses = computed(() => ({
    sm: "text-sm px-3 py-1",
    md: "text-base px-4 py-2",
    lg: "text-lg px-5 py-3",
  }));
  </script>