<script setup lang="ts">
const username = ref('')
const password = ref('')
const role = ref<string | null>(null)
    
const handleLogin = () => {
    if (username.value === 'admin' && password.value === '123') {
    role.value = 'Administrator'
  } else if (username.value === 'uczen' && password.value === '123') {
    role.value = 'Uczeń'
  } else {
    alert('Błędne dane! Użyj admin/123 lub uczen/123')
  }
}</script>

<template>
   <div class="min-h-screen bg-slate-900 text-white flex items-center justify-center font-sans">
    <div class="bg-slate-800 p-8 rounded-2xl shadow-xl w-full max-w-md border border-slate-700">
      <h1 class="text-3xl font-bold mb-6 text-center text-blue-400">Merito GOŁ</h1>
      
      <div v-if="!role" class="flex flex-col gap-4">
        <label class="text-sm text-slate-400">Zaloguj się, aby zarządzać ocenami</label>
        <input v-model="username" type="text" placeholder="Login (admin / uczen)" 
               class="p-3 rounded bg-slate-700 border border-slate-600 focus:border-blue-500 outline-none transition" />
        <input v-model="password" type="password" placeholder="Hasło (123)" 
               class="p-3 rounded bg-slate-700 border border-slate-600 focus:border-blue-500 outline-none transition" />
        <button @click="handleLogin" 
                class="bg-blue-600 hover:bg-blue-700 p-3 rounded font-bold transition shadow-lg mt-2">
          Zaloguj się
        </button>
      </div>

      <div v-else class="text-center">
        <div class="mb-6">
          <p class="text-lg">Witaj z powrotem,</p>
          <p class="text-2xl font-black text-blue-400 uppercase tracking-wider">{{ role }}</p>
        </div>
        
        <div class="p-4 bg-slate-700/50 rounded-lg border border-slate-600 mb-6">
          <p v-if="role === 'Administrator'" class="text-sm">
            Masz uprawnienia do wystawiania ocen w module cateringowym.
          </p>
          <p v-else class="text-sm">
            Możesz przeglądać swoje oceny i jadłospis.
          </p>
        </div>

        <button @click="role = null" class="text-sm text-slate-500 hover:text-white underline transition">
          Wyloguj się
        </button>
      </div>
    </div>
  </div></template>
