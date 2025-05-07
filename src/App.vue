<script setup>
import { ref, computed } from 'vue'

const tugas = ref([])
const input = ref('')
const filterr = ref('all')

const jumlahTugas = computed(() => {
  return tugas.value.filter((tugas) => !tugas.status).length
})

function tambahTugas() {
  if (input.value.trim() !== '') {
    tugas.value.push({
      id: Date.now(),
      text: input.value,
      status: false
    })
    input.value = ''
  }
}

const hapusTugas = (id) => {
  tugas.value = tugas.value.filter((tugas) => tugas.id !== id)
}

const filterTugas = computed(() => {
  if (filterr.value === 'all') return tugas.value
  if (filterr.value === 'active') return tugas.value.filter((t) => !t.status)
  if (filterr.value === 'completed') return tugas.value.filter((t) => t.status)
})
</script>

<template>
  <div class="min-h-screen bg-gray-900 text-white flex items-center justify-center p-6">
    <div class="w-full max-w-xl bg-gray-800 rounded-xl shadow-lg p-6 space-y-6">
      <h1 class="text-3xl font-bold text-green-400 text-center">Manajemen Tugas</h1>

      <div class="flex gap-2">
        <input
          v-model="input"
          @keyup.enter="tambahTugas"
          placeholder="Tambah tugas baru..."
          class="flex-1 p-2 rounded-md bg-gray-700 text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-green-400"
        />
        <button
          @click="tambahTugas"
          class="bg-green-500 hover:bg-green-600 px-4 py-2 rounded-md font-medium transition"
        >
          Tambah
        </button>
      </div>

      <div class="flex justify-between">
        <select
          v-model="filterr"
          class="bg-gray-700 text-white px-3 py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-green-400"
        >
          <option value="all">Semua</option>
          <option value="active">Aktif</option>
          <option value="completed">Selesai</option>
        </select>
        <p class="text-sm text-gray-300">Tugas Aktif: {{ jumlahTugas }}</p>
      </div>

      <ul class="space-y-3 h-75 overflow-y-auto pr-2">
        <li
          v-for="tugas in filterTugas"
          :key="tugas.id"
          class="flex justify-between items-center bg-gray-700 px-4 py-2 rounded-md"
        >
          <div class="flex items-center gap-3">
            <input
              type="checkbox"
              v-model="tugas.status"
              class="accent-green-500 w-5 h-5"
            />
            <span :class="{ 'line-through text-gray-400': tugas.status }">
              {{ tugas.text }}
            </span>
          </div>
          <button
            @click="hapusTugas(tugas.id)"
            class="text-red-400 hover:text-red-600 font-bold"
          >
            Hapus
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
/* Optional: custom scrollbar */
ul::-webkit-scrollbar {
  width: 6px;
}
ul::-webkit-scrollbar-thumb {
  background-color: #4ade80;
  border-radius: 6px;
}
</style>
