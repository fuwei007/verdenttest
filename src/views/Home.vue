<template>
  <div class="home-container">
    <h1>Welcome, {{ user.name }}!</h1>
    <p>You are logged in as {{ user.email }}</p>
    <button @click="logout">Logout</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const user = ref(JSON.parse(localStorage.getItem('user') || '{}'))

function logout() {
  localStorage.removeItem('user')
  router.push('/login')
}
</script>

<style scoped>
.home-container {
  max-width: 500px;
  margin: 80px auto;
  padding: 32px;
  text-align: center;
}
button {
  margin-top: 24px; padding: 12px 32px; background: #e74c3c; color: white;
  border: none; border-radius: 4px; cursor: pointer; font-size: 16px;
}
button:hover { background: #c0392b; }
</style>
