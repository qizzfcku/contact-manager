<template>
  <div class="p-4 border rounded shadow-sm flex justify-between items-center">
    <p>{{ contact.name }} - {{ contact.phone }} - {{ contact.email }}</p>
    <div>
      <button @click="$emit('edit')" class="bg-blue-500 text-white px-2 py-1 rounded mr-2">Редактировать</button>
      <button @click="$emit('delete')" class="bg-red-500 text-white px-2 py-1 rounded">Удалить</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

interface Contact {
  id: number;
  name: string;
  phone: string;
  email: string;
}

export default defineComponent({
  name: 'ContactItem',
  props: {
    contact: {
      type: Object as PropType<Contact>,
      required: true
    }
  }
})
</script>

<style>
</style>
