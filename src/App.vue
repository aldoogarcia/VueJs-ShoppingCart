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

const saveItemp = ()=> {
  //Agraga un nuevo objeto a la lista
  items.value.push({id: items.value.length, label:newItem.value});
  //borra el contenido de la caja de texto
  newItem.value= "";
};

</script>
<template>
<form v-on:submit.prevent="saveItemp" class="add-item form">
  <h1>🛒 App lista de compras</h1>
  <div class="add-item form">
    <input  v-model="newItem" type="text" placeholder="Agregar articulo">
    <label><input type="checkbox" v-model="newItem">Alta prioridad</label>
    <br>
    <!--Buton-->
    <button class="btn btn-primary" >Agregar articulo</button>
  </div>
  <!--Checkbox-->
</form>
<ul>
  <li v-for="({id,label},i)  in items" v-bind:key="id">🛒 {{ label }} 
  </li>
</ul>

</template>


