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
  <body class="w-screen h-screen flex justify-center items-center bg-slate-100">
    <container class="w-[80%] h-[80vh] flex shadow-2xl">
      <section class="w-[50%] flex justify-center items-center bg-orange-400"></section>

      <section class="w-[50%] flex justify-center items-center bg-white">
        <Form
          v-slot="$form"
          :resolver="resolver"
          @submit="onFormSubmit"
          :initialValues
          class="flex flex-col gap-4 w-[50%]"
        >
          <InputText name="username" type="text" placeholder="Username" fluid />
          <Message v-if="$form.username?.invalid" severity="error" size="small" variant="simple">{{
            $form.username.error.message
          }}</Message>

          <Password name="password" placeholder="Password" :feedback="false" toggleMask fluid />
          <Message v-if="$form.password?.invalid" severity="error" size="small" variant="simple">{{
            $form.password.error.message
          }}</Message>

          <Button type="submit" severity="secondary" label="Submit" />
        </Form>
      </section>
    </container>
  </body>
</template>
