<!-- eslint-disable vue/no-parsing-error -->
<script setup>
//Computed solo lanzan una nueva version, trabana con funciones que retornan
import { ref, computed } from 'vue'
const items = ref([
  //  { id: 1, label: "Leche",purchased:false,highPriority:true }, // Unique IDs and capitalized label
  //  { id: 2, label: "Carne",purchased:true ,highPriority:false},
  //  { id: 3, label: "Arroz",purchased:false,highPriority:true },
  //  { id: 4, label: "Pezcado",purchased:false,highPriority:false }
]);

//computed tiene que retonrnar un valor | ... son para clonar el array
const reversedItems=computed(()=>{
  return[...items.value].reverse();
})
//cambia para el estado de compra
const togglePurchased=(item)=>{
  item.purchased=!item.purchased;
}
const header=ref("Lista de compras");
const newItem= ref("");
//Creando propiedad computada
const characterCount=computed(()=>{
  return newItem.value.length;
});
const newItemhigt= ref("");

const saveItemp = ()=> {
  //Agraga un nuevo objeto a la lista
  items.value.push({id: items.value.length, label:newItem.value, highPriority: newItemhigt.value});
  //borra el contenido de la caja de texto
  newItem.value= "";
  newItemhigt.value=false
};

const mostrar = ref(false);
const mostrarOcultar=(condicion)=>{
  mostrar.value=condicion;
}
//Vacia la lista
const eliminarArray=ref(()=>{
  items.value=[];

});

//limita numero de caracteres escritos
const limitaCaracteres=ref(()=>{
  if(newItem.value.length>10){
    newItem.value=newItem.value.substring(0,10);
    alert("Maximo de caracteres");
    
  }
})

//elimina el ultimo objeto agregado
const eliinarUltimo=ref(()=>{
  return items.value.pop()
}
)
</script>

<template>
  <!-- head -->
  <div class="header">
    <h1>
      🛒 {{ header }}
    </h1>
    <button v-on:click="mostrarOcultar(false)" v-if="mostrar" class="btn">Cancelar</button>
    <button  v-on:click="mostrarOcultar(true)" v-else class="btn btn-primary">Agregar</button>
  </div>
 
  <!-- Formulario -->
<form v-if="mostrar" v-on:submit.prevent="saveItemp" class="add-item form">
  {{ limitaCaracteres() }}
  <div class="add-item form">
    <input  v-model="newItem" type="text" placeholder="Agregar articulo">
    <label><input type="checkbox" v-model="newItemhigt">Alta prioridad</label>
    <!--Buton-->
    <button id="agregar" class="btn btn-primary" >Agregar articulo</button>
    <p class="count">
      {{ characterCount }} /10
    </p>
  </div>
  <!--Checkbox-->
</form>
<!--Entrega de lista  -->
<ul>
  <li v-for="({id,label,purchased,highPriority},i)  in reversedItems"
  @click="togglePurchased(reversedItems[i])"
  :class="{priority:highPriority, strikeout:purchased}"
  v-bind:key="id">🛒 {{ label }} 
  </li>
</ul>
<!-- <ul>
  <li v-for="({id,label,purchased,highPriority},i)  in items"
  :class="[purchased?'strikeout':'',highPriority?'priority':'']"
  v-bind:key="id">🛒 {{ label }} 
  </li>
</ul> -->
<!-- Mensaje condicional -->
<p v-if="items.length===0">No hay elementos en la lista 🥀</p>
<button @click="eliminarArray" class="btn btn-cancel">Vaciar Lista</button>
<button v-on:click="eliinarUltimo" class="btn btn-cancel">Eliminar</button>
</template>