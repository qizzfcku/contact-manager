<template>
  <div class="mb-4">
    <input
      type="text"
      placeholder="Поиск контактов"
      v-model="query"
      @input="handleInput"
      class="border p-2 w-full"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'SearchBar',
  emits: ['search'],
  setup (_, { emit }) {
    const query = ref('')

    const handleInput = () => {
      emit('search', query.value)
    }

    return { query, handleInput }
  }
})
</script>
