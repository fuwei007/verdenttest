<template>
  <div class="auth-container">
    <h2>Login</h2>
    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label>Email2</label>
        <input v-model="email" type="email" required placeholder="Enter your email" />
      </div>
      <div class="form-group">
        <label>Password</label>
        <input v-model="password" type="password" required placeholder="Enter your password" />
      </div>
      <p v-if="error" class="error">{{ error }}</p>
      <button type="submit">Login</button>
    </form>
    <p class="link">Don't have an account? <router-link to="/signup">Sign Up</router-link></p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const error = ref('')
const router = useRouter()

function handleLogin() {
  const users = JSON.parse(localStorage.getItem('users') || '[]')
  const user = users.find(u => u.email === email.value && u.password === password.value)
  if (user) {
    localStorage.setItem('user', JSON.stringify(user))
    router.push('/home')
  } else {
    error.value = 'Invalid email or password'
  }
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
.link { text-align: center; margin-top: 16px; }
</style>
