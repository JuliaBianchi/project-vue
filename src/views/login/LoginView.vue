<script setup lang="ts">
import LoginForm from '@/components/LoginForm.vue'
import RegisterForm from '@/components/RegisterForm.vue'
import { Button } from 'primevue'
import { ref } from 'vue'

const currentForm = ref<string>('login')

const toggleForm = () => {
  currentForm.value = currentForm.value === 'login' ? 'register' : 'login'
}
</script>

<template>
  <body class="w-screen h-screen flex justify-center items-center bg-slate-100">
    <div class="w-[80%] h-[80vh] flex shadow-2xl">
      <section class="w-[50%] flex justify-center items-center"></section>

      <section class="w-[50%] flex flex-col justify-center items-center bg-white">

        <div class="w-[70%]" v-if="currentForm.toLowerCase() === 'login'">
          <LoginForm />

          <div class="flex justify-center flex-row items-center pt-10">
            <p class="text-black text-md">Não tem conta?</p>

            <Button label="Cadastre-se" @click="toggleForm" variant="link" />
          </div>
        </div>

        <div class="w-[65%]" v-else>
          <RegisterForm />

          <div class="flex justify-center flex-row items-center pt-10">
            <p class="text-black text-md">Já tem uma conta?</p>

            <Button label="Entrar" @click="toggleForm" variant="link" />
          </div>
        </div>
      </section>
    </div>
  </body>
</template>
