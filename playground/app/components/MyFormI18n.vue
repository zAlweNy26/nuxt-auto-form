<script setup lang="ts">
import { AInputWithClear } from '#components'
import * as z from 'zod'

const ENUM_MULTIPLE = [
  'A',
  'B',
  'C',
  'D',
  'E',
  'F',
]

const schema = z.object({
  text: z.string()
    .nonempty()
    .meta({
      title: 'form.text',
      i18n: true,
      required: true,
      input: {
        props: {
          placeholder: 'Placeholder',
        },
      },
    }),
  email: z.email()
    .nonempty(),
  enum: z.enum(['1', '2', '3'])
    .meta({
      title: 'form.enum',
      i18n: true,
    }),
  text_description: z.string()
    .meta({
      description: 'form.description',
      i18n: true,
      hint: 'with hint',
      input: {
        component: AInputWithClear,
      },
    }),
  custom_bool: z.boolean()
    .meta({ title: 'Input with custom slot' }),
  bool: z.boolean()
    .default(true)
    .meta({
      title: 'form.bool',
      i18n: true,
      theme: { floatRight: true },
    }),
  multiple_input: z
    .array(z.enum(ENUM_MULTIPLE))
    .meta({ title: 'Multiple Enum Input' }),
})

function onSubmit(data: Record<string, any>) {
  useToast().add({
    title: 'Form submitted',
    description: JSON.stringify(data, null, 2),
  })
}
</script>

<template>
  <AutoForm
    :schema="schema"
    @submit="onSubmit"
  >
    <template #text-hint>
      <NuxtLink to="https://norbiros.dev">
        Who?
      </NuxtLink>
    </template>
    <template #custom_bool="{ field, state }">
      <USelect
        v-model="state[field]"
        :items="[
          {
            label: 'False',
            value: false,
          },
          {
            label: 'True',
            value: true,
          },
        ]"
      />
    </template>
  </AutoForm>
</template>
