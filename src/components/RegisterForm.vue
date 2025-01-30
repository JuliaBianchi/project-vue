<script setup lang="ts">
import Button from 'primevue/button'
import { InputText, Message, Password } from 'primevue'
import { ref } from 'vue'
import { Form } from '@primevue/forms'
import { zodResolver } from '@primevue/forms/resolvers/zod'
import { z } from 'zod'

const initialValues = ref({
  name: '',
  email: '',
  phone: '',
  password: '',
  confirmPassword: '',
})

const resolver = zodResolver(
  z
    .object({
      name: z.string().min(1, { message: "Nome é obrigatório." }),
      email: z.string().email({ message: "E-mail inválido." }).min(1, { message: "E-mail é obrigatório." }),
      phone: z.string().min(1, { message: "Telefone é obrigatório." }),
      password: z.string().min(8, { message: "A senha deve ter no mínimo 8 caracteres." }),
      confirmPassword: z.string().min(8, { message: "A senha deve ter no mínimo 8 caracteres." }),
    })
    .refine(
      (data) => data.password === data.confirmPassword,
      {
        message: "As senhas não coincidem.",
        path: ["confirmPassword"],
      }
    )
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
    class="flex flex-col gap-4"
  >


    <div class="overflow-y-auto max-h-90 flex flex-col gap-5 p-4 rounded-lg">
      <InputText name="name" type="text" placeholder="Nome" fluid />
      <Message v-if="$form.name?.invalid" severity="error" size="small" variant="simple">
        {{ $form.name.error.message }}
      </Message>

      <InputText name="email" type="text" placeholder="E-mail" fluid />
      <Message v-if="$form.email?.invalid" severity="error" size="small" variant="simple">
        {{ $form.email.error.message }}
      </Message>

      <InputText name="phone" type="text" placeholder="Telefone" fluid />
      <Message v-if="$form.phone?.invalid" severity="error" size="small" variant="simple">
        {{ $form.phone.error.message }}
      </Message>

      <Password name="password" type="text" placeholder="Senha" :feedback="false" toggleMask fluid />
      <Message v-if="$form.password?.invalid" severity="error" size="small" variant="simple">
        {{ $form.password.error.message }}
      </Message>

      <Password name="confirmPassword" type="text" placeholder="Confirmar Senha" :feedback="false" toggleMask fluid />
      <Message v-if="$form.confirmPassword?.invalid" severity="error" size="small" variant="simple">
        {{ $form.confirmPassword.error.message }}
      </Message>
    </div>

    <Button type="submit" severity="primary" label="Cadastrar" />
  </Form>
</template>
