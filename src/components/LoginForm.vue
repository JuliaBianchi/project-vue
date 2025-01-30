<script setup lang="ts">
import Button from 'primevue/button'
import { InputText, Message, Password } from 'primevue'
import { ref } from 'vue'
import { Form } from '@primevue/forms'
import { zodResolver } from '@primevue/forms/resolvers/zod'
import { z } from 'zod'


const initialValues = ref({
  username: '',
  password: '',
})

const resolver = zodResolver(
  z.object({
    username: z.string().min(1, { message: 'Nome de usuário é obrigatório.' }),
    password: z.string().min(1, { message: 'Senha é obrigatória.' }),
  }),
)

const onFormSubmit = (e: { valid: unknown }) => {
  if (e.valid) {
  }
}
</script>

<template>

        <Form
          v-slot="$form"
          :resolver="resolver"
          @submit="onFormSubmit"
          :initialValues
          class="flex flex-col gap-6 "
          >

          <InputText name="username" type="text" placeholder="Usuário" fluid />
          <Message v-if="$form.username?.invalid" severity="error" size="small" variant="simple">{{ $form.username.error.message }}</Message>

          <Password name="password" placeholder="Senha" :feedback="false" toggleMask fluid />
          <Message v-if="$form.password?.invalid" severity="error" size="small" variant="simple">{{ $form.password.error.message }}</Message>

          <router-link to="/esqueceu-senha" class="text-md self-end">
            Esqueceu a senha?
          </router-link>

          <Button type="submit" severity="secondary" label="Entrar" />

        </Form>

</template>

