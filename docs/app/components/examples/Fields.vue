<script setup lang="ts">
import * as z from 'zod'

const schema = z.object({
  form_field: z.string()
    .nonempty()
    .meta({
      title: 'Title',
      required: true,
      description: 'Description',
      hint: 'Hint',
      help: 'Help',
    }),
  input: z.number().meta({
    title: 'input.title',
    description: 'input.description',
    hint: 'input.hint',
    help: 'input.help',
    i18n: true,
    input: {
      props: {
        placeholder: '69420',
      },
    },
  }),
  style: z.boolean()
    .meta({ theme: { floatRight: true } }),
})
</script>

<template>
  <AutoForm :schema="schema" />
</template>
