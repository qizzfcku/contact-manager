<template>
  <div id="app" class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Управление контактами</h1>
    <SearchBar @search="searchContacts" />
    <ContactForm @save="saveContact" :editingContact="editingContact" />
    <ContactList
      :contacts="filteredContacts"
      @edit="editContact"
      @delete="deleteContact"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import ContactList from './components/ContactList.vue'
import ContactForm from './components/ContactForm.vue'
import SearchBar from './components/SearchBar.vue'

interface Contact {
  id: number;
  name: string;
  phone: string;
  email: string;
}

export default defineComponent({
  name: 'App',
  components: {
    ContactList,
    ContactForm,
    SearchBar
  },
  setup () {
    const contacts = ref<Contact[]>(JSON.parse(localStorage.getItem('contacts') || '[]'))
    const searchQuery = ref('')
    const editingContact = ref<Contact | null>(null)

    const saveContact = (contact: Contact) => {
      if (contact.id) {
        const index = contacts.value.findIndex(c => c.id === contact.id)
        contacts.value.splice(index, 1, contact)
      } else {
        contact.id = Date.now()
        contacts.value.push(contact)
      }
      localStorage.setItem('contacts', JSON.stringify(contacts.value))
    }

    const editContact = (contact: Contact) => {
      editingContact.value = contact
    }

    const deleteContact = (id: number) => {
      contacts.value = contacts.value.filter(contact => contact.id !== id)
      localStorage.setItem('contacts', JSON.stringify(contacts.value))
    }

    const searchContacts = (query: string) => {
      searchQuery.value = query
    }

    const filteredContacts = computed(() => {
      return contacts.value.filter(contact =>
        contact.name.toLowerCase().includes(searchQuery.value.toLowerCase())
      )
    })

    return {
      contacts,
      searchQuery,
      editingContact,
      saveContact,
      editContact,
      deleteContact,
      searchContacts,
      filteredContacts
    }
  }
})
</script>

<style>
</style>
