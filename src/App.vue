<script setup>
import { ref } from 'vue'

const tugas = ref([
  { id: 1, text: 'makan', status: 'Belum Selesai' },
  { id: 2, text: 'minum', status: 'Selesai' },
  { id: 3, text: 'joging', status: 'Belum Selesai' },
])

const input = ref('')

function tambahTugas() {
  if (input.value !== '') {
    tugas.value.push({
      id: tugas.value.length + 1,
      text: input.value,
      status: 'Belum Selesai'
    })
    input.value = ''
  }
}
</script>

<template>
  <div>
    <h1>Tugas</h1>
    <input type="text" @keyup.enter="tambahTugas" v-model="input" placeholder="Tambah tugas">
    <button @click="tambahTugas">Tambah</button>
    <ul>
      <li v-for="tugas in tugas" :key="tugas.id">
        {{ tugas.text }} - {{ tugas.status }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
