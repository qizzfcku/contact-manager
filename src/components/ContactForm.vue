<template>
  <div class="mb-4">
    <h2 class="text-xl font-semibold mb-2">{{ editingContact ? 'Редактировать контакт' : 'Добавить новый контакт' }}</h2>
    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div>
        <label for="name" class="block">Имя:</label>
        <input v-model="form.name" type="text" id="name" required class="border p-2 w-full" />
      </div>
      <div>
        <label for="phone" class="block">Телефон:</label>
        <input v-model="form.phone" type="tel" id="phone" required class="border p-2 w-full" />
      </div>
      <div>
        <label for="email" class="block">Email:</label>
        <input v-model="form.email" type="email" id="email" required class="border p-2 w-full" />
      </div>
      <button type="submit" class="bg-green-500 text-white px-4 py-2 rounded">Сохранить</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'

interface Contact {
  id: number;
  name: string;
  phone: string;
  email: string;
}

export default defineComponent({
  name: 'ContactForm',
  props: {
    editingContact: {
      type: Object as () => Contact | null,
      default: null
    }
  },
  emits: ['save'],
  setup (props, { emit }) {
    const form = ref<Contact>({
      id: 0,
      name: '',
      phone: '',
      email: ''
    })

    watch(() => props.editingContact, (newVal) => {
      if (newVal) {
        form.value = { ...newVal }
      } else {
        form.value = { id: 0, name: '', phone: '', email: '' }
      }
    })

    const handleSubmit = () => {
      emit('save', form.value)
      form.value = { id: 0, name: '', phone: '', email: '' }
    }

    return { form, handleSubmit }
  }
})
</script>

<style>
</style>
