<script setup>
import { ref } from 'vue'
const items = ref([
  { id: 1, label: "Leche" }, // Unique IDs and capitalized label
  { id: 2, label: "Carne" },
  { id: 3, label: "Arroz" },
  { id: 3, label: "Pezcado" }
]);
</script>

<template>
  <ul>
    <li v-for="item in items" :key="item.id"> {{ item.label }}
    </li>
  </ul>
</template>


