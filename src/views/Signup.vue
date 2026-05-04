<template>
  <div class="auth-container">
    <h2>Sign Up</h2>
    <form @submit.prevent="handleSignup">
      <div class="form-group">
        <label>Name</label>
        <input v-model="name" type="text" required placeholder="Enter your name" />
      </div>
      <div class="form-group">
        <label>Email</label>
        <input v-model="email" type="email" required placeholder="Enter your email" />
      </div>
      <div class="form-group">
        <label>Password</label>
        <input v-model="password" type="password" required placeholder="Create a password" />
      </div>
      <p v-if="error" class="error">{{ error }}</p>
      <p v-if="success" class="success">{{ success }}</p>
      <button type="submit">Sign Up</button>
    </form>
    <p class="link">Already have an account? <router-link to="/login">Login</router-link></p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const name = ref('')
const email = ref('')
const password = ref('')
const error = ref('')
const success = ref('')
const router = useRouter()

function handleSignup() {
  const users = JSON.parse(localStorage.getItem('users') || '[]')
  if (users.find(u => u.email === email.value)) {
    error.value = 'Email already registered'
    success.value = ''
    return
  }
  users.push({ name: name.value, email: email.value, password: password.value })
  localStorage.setItem('users', JSON.stringify(users))
  success.value = 'Account created! Redirecting to login...'
  error.value = ''
  setTimeout(() => router.push('/login'), 1500)
}
</script>

<style scoped>
.auth-container {
  max-width: 400px;
  margin: 80px auto;
  padding: 32px;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}
h2 { text-align: center; margin-bottom: 24px; }
.form-group { margin-bottom: 16px; }
.form-group label { display: block; margin-bottom: 4px; font-weight: 500; }
.form-group input {
  width: 100%; padding: 10px; border: 1px solid #ddd;
  border-radius: 4px; box-sizing: border-box;
}
button {
  width: 100%; padding: 12px; background: #42b883; color: white;
  border: none; border-radius: 4px; cursor: pointer; font-size: 16px;
}
button:hover { background: #38a373; }
.error { color: red; font-size: 14px; }
.success { color: green; font-size: 14px; }
.link { text-align: center; margin-top: 16px; }
</style>
