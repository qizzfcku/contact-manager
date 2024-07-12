<template>
  <div class="mt-4">
    <div v-for="contact in contacts" :key="contact.id" class="mb-2">
      <ContactItem
        :contact="contact"
        @edit="() => $emit('edit', contact)"
        @delete="() => $emit('delete', contact.id)"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import ContactItem from './ContactItem.vue'

interface Contact {
  id: number;
  name: string;
  phone: string;
  email: string;
}

export default defineComponent({
  name: 'ContactList',
  components: { ContactItem },
  props: {
    contacts: {
      type: Array as PropType<Contact[]>,
      required: true
    }
  }
})
</script>

<style>
</style>
