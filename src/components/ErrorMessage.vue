<template>
    <div v-if="error" class="alert alert-danger" role="alert">
      {{ error }}
    </div>
  </template>
  
  <script>
  export default {
    props: {
      error: {
        type: String,
        required: true
      }
    }
  };
  </script>
  