<script setup>
import { ref, computed } from 'vue'

const tugas = ref([
  { id: 1, text: 'makan', status: false },
  { id: 2, text: 'minum', status: true },
  { id: 3, text: 'joging', status: false },
])

const input = ref('')

const jumlahTugas = computed(() => {
  return tugas.value.filter((tugas) => tugas.status === false).length
})

function tambahTugas() {
  if (input.value !== '') {
    tugas.value.push({
      id: tugas.value.length + 1,
      text: input.value,
      status: false
    })
    input.value = ''
  }
}

const hapusTugas = (id) => {
  tugas.value = tugas.value.filter((tugas) => tugas.id !== id)
}



</script>

<template>
  <div>
    <h1>Tugas</h1>
    <input type="text" @keyup.enter="tambahTugas" v-model="input" placeholder="Tambah tugas">
    <button @click="tambahTugas">Tambah</button>
    <ul>
      <li v-for="tugas in tugas" :key="tugas.id">
        <input type="checkbox" v-model="tugas.status">
        {{ tugas.text }} - {{ tugas.status }}
        <button @click="hapusTugas(tugas.id)">Hapus</button>
      </li>
    </ul>
    <p>Jumlah tugas aktif: {{ jumlahTugas }}</p>
  </div>
</template>

<style scoped></style>
