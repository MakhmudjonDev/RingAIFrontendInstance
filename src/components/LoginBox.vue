<template>
    <div class="container">
      <div class="gray-box">
        <h2>Login</h2>
        <form @submit.prevent="login">
          <div class="form-group">
            <label for="username">Username:</label>
            <input type="text" id="username" v-model="username" required>
          </div>
          <div class="form-group">
            <label for="password">Password:</label>
            <input type="password" id="password" v-model="password" required>
          </div>
          <button type="submit" class="button gray-button">Login</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        username: '',
        password: ''
      };
    },
    methods: {
      login() {
        // Implement your login logic here
        console.log('Username:', this.username);
        console.log('Password:', this.password);
        // After successful login, you can redirect the user to another page
      }
    }
  };
  </script>
  
  <style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh; /* Minimum height of 100% of the viewport height */
  }
  
  .gray-box {
    background-color: #f2f2f2;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    width: 70%; /* Adjust the width as needed */
    max-width: 400px; /* Maximum width for better readability */
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
  }
  
  input[type="text"],
  input[type="password"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  
  button {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background-color: #ccc;
  }
  
  button:hover {
    background-color: #aaa;
  }
  </style>
  