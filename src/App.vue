<!-- eslint-disable vue/no-parsing-error -->
<script setup>
import { ref } from 'vue'

const items = ref([
  //{ id: 1, label: "Leche" }, // Unique IDs and capitalized label
  //{ id: 2, label: "Carne" },
  //{ id: 3, label: "Arroz" },
  //{ id: 4, label: "Pezcado" }
]);

const newItem= ref("");

const saveItemp = ()=> {
  //Agraga un nuevo objeto a la lista
  items.value.push({id: items.value.length, label:newItem.value});
  //borra el contenido de la caja de texto
  newItem.value= "";
};

const mostrar = ref(false);
const mostrarOcultar=(condicion)=>{
  mostrar.value=condicion;
}
</script>

<template>
  <!-- head -->
  <div class="header">
    <h1>
      🛒 App lista de compras
    </h1>
    <button v-on:click="mostrarOcultar(false)" v-if="mostrar" class="btn">Cancelar</button>
    <button v-on:click="mostrarOcultar(true)" v-else class="btn btn-primary">Agregar</button>
  </div>
 
  <!-- Formulario -->
<form v-if="mostrar" v-on:submit.prevent="saveItemp" class="add-item form">
  
  <div class="add-item form">
    <input  v-model="newItem" type="text" placeholder="Agregar articulo">
    <label><input type="checkbox" v-model="newItem">Alta prioridad</label>
    <!--Buton-->
    <button class="btn btn-primary" >Agregar articulo</button>
  </div>
  <!--Checkbox-->
</form>
<!--Entrega de lista  -->
<ul>
  <li v-for="({id,label},i)  in items" v-bind:key="id">🛒 {{ label }} 
  </li>
</ul>
<!-- Mensaje condicional -->
<p v-if="items.length===0">No hay elementos en la lista 🥀</p>
</template>