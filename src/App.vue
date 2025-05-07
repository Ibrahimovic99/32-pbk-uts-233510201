<script setup>
import { ref } from 'vue'

const tugas = ref([
  { id: 1, text: 'makan', status: 'Belum Selesai' },
  { id: 2, text: 'minum', status: 'Selesai' },
  { id: 3, text: 'joging', status: 'Belum Selesai' },
])
</script>

<template>
  <div>
    <h1>Tugas</h1>
    <ul>
      <li v-for="tugas in tugas" :key="tugas.id">
        {{ tugas.text }} - {{ tugas.status }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
