<template>
    <div id="app">
      <SpinnerWheel />
    </div>
  </template>
  
  <script>
  import SpinnerWheel from './components/SpinnerWheel.vue';
  
  export default {
    components: {
      SpinnerWheel,
    },
  };
  </script>
  
  <style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #dcd9d9;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }
  </style>
  