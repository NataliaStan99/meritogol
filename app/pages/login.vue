<script setup lang="ts">
import { ref } from 'vue'

interface Ocena {
  id: number;
  student: string;
  przedmiot: string;
  ocena: number;
}

const username = ref('')
const password = ref('')
const role = ref<string | null>(null)

const { data: oceny } = await useFetch<Ocena[]>('/api/oceny')

const handleLogin = () => {
  if (username.value === 'Natalia61870' && password.value === 'Meritogo') {
    role.value = 'Administrator'
  } else if (username.value === 'uczen' && password.value === '123') {
    role.value = 'Uczeń'
  } else {
    alert('Błędne dane! Spróbuj Natalia61870 / Meritogo')
  }
}
</script>

<template>
  <div class="min-h-screen bg-slate-900 text-white flex items-center justify-center font-sans p-4">
    <div class="bg-slate-800 p-8 rounded-2xl shadow-xl w-full max-w-md border border-slate-700">
      <h1 class="text-3xl font-bold mb-6 text-center text-blue-400 tracking-tight">Merito GOŁ</h1>

      <div v-if="!role" class="flex flex-col gap-4">
        <label class="text-sm text-slate-400">Zaloguj się, aby zarządzać ocenami</label>
        
        <input 
          v-model="username" 
          type="text" 
          placeholder="Login" 
          class="p-3 rounded bg-slate-700 border border-slate-600 focus:border-blue-500 outline-none transition"
        />
        
        <input 
          v-model="password" 
          type="password" 
          placeholder="Hasło" 
          class="p-3 rounded bg-slate-700 border border-slate-600 focus:border-blue-500 outline-none transition"
        />
        
        <button 
          @click="handleLogin" 
          class="bg-blue-600 hover:bg-blue-700 p-3 rounded font-bold transition shadow-lg mt-2"
        >
          Zaloguj się
        </button>
      </div>

      <div v-else class="text-center">
        <div class="mb-6">
          <p class="text-lg text-slate-300">Witaj z powrotem,</p>
          <p class="text-3xl font-black text-blue-400 uppercase tracking-tighter">{{ role }}</p>
        </div>
        
        <div class="p-4 bg-slate-700/30 rounded-lg border border-slate-700 mb-6">
          <p class="text-sm text-slate-300">
            Masz uprawnienia do przeglądania dziennika ocen.
          </p>
        </div>

        <div v-if="oceny" class="mt-6 text-left border-t border-slate-700 pt-6">
          <p class="text-blue-400 font-bold mb-4 text-xs uppercase tracking-widest text-center">Aktualne wyniki w systemie:</p>
          <div class="space-y-3">
            <div v-for="o in oceny" :key="o.id" class="bg-slate-700/50 p-3 rounded-xl flex justify-between items-center border border-slate-600">
              <div class="flex flex-col">
                <span class="text-white font-medium text-sm">{{ o.student }}</span>
                <span class="text-slate-400 text-[10px]">{{ o.przedmiot }}</span>
              </div>
              <span class="bg-blue-500/20 text-blue-400 px-3 py-1 rounded-full text-xs font-black border border-blue-500/30">
                {{ o.ocena }}
              </span>
            </div>
          </div>
        </div>

        <button 
          @click="role = null" 
          class="mt-8 text-xs text-slate-500 hover:text-white underline transition opacity-70"
        >
          Wyloguj się
        </button>
      </div>
    </div>
  </div>
</template>