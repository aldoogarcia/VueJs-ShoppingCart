<!-- eslint-disable vue/no-parsing-error -->
<script setup>
import { ref } from 'vue'

const items = ref([
  { id: 1, label: "Leche" }, // Unique IDs and capitalized label
  { id: 2, label: "Carne" },
  { id: 3, label: "Arroz" },
  { id: 4, label: "Pezcado" }
]);

const newItem= ref("");


</script>

<template>
  <h1>🛒 App lista de compras</h1>
  <div class="add-item form">
    <input v-model="newItem" type="text" placeholder="Agregar articulo">
    <label><input type="checkbox" v-model="newItem">Alta prioridad</label>
    <br>
    <!--Buton-->
    <button class="btn btn-primary" v-on:click="items.push({id: items.length, label:newItem})">Agregar articulo</button>
  </div>
  <!--Checkbox-->

  <ul>
    <li v-for="({id,label},i)  in items" v-bind:key="id">🛒 {{ label }} 
    </li>
  </ul>
</template>


