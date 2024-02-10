<template> 
  <div> 
    <br>
    <h1>Perfumes existentes y agrega perfumes</h1>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Acordes</th>
        </tr>
      </thead>
      <tr>
        <td>{{ obtenerProximoId() }}</td>
        <td><input v-model="nuevoPerfume.nombre" type="text" placeholder="Nombre" required /></td>
        <td><input v-model="nuevoPerfume.price" type="number" placeholder="Precio" required /></td>
        <td><input v-model="nuevoPerfume.acordes" type="text" placeholder="Acordes" required /></td>
        <td><button type="submit" @click.prevent="agregarNuevoPerfume" class="Button">Agregar Perfume</button></td>
      </tr>

      <tbody>
        <PerfumeItem
        v-bind="perfume"
        v-for="perfume in perfumesmostrar"
        :key="perfume.id"
        @click="seleccionarPerfume(perfume.id)"
        :perfume="perfume"
        :class="{ 'selected': perfume.id === Sombra }"
        @SayHi="onSayHi" />

      </tbody>
    </table>
      <br>
     </div>
</template>

<script setup lang="ts"> //Realizado por Luis Fentes
import PerfumeDatos from '../../datos/PerfumeDatos'
import { ref } from 'vue';
import PerfumeItem from './PerfumeItem.vue';
import type { IPerfume } from '@/interface/IPerfume';

const nuevoPerfume = ref<IPerfume>({
  id: 0, 
  nombre: '',
  price: 0,
  acordes: ''
});

const perfumesmostrar = ref<IPerfume[]>([]);
perfumesmostrar.value = PerfumeDatos;

// Estado para almacenar el ID del perfume seleccionado
const Sombra = ref<number | null>(null);

// Función para seleccionar un perfume al hacer clic en él
const seleccionarPerfume = (id: number) => {
    Sombra.value = id;
};

// Función para encontrar el último ID y establecer el próximo ID automáticamente
const obtenerProximoId = () => {
  const ultimoId = perfumesmostrar.value.reduce((maxId, perfume) => {
    return perfume.id > maxId ? perfume.id : maxId;
  }, 0);
  return ultimoId + 1;
};

// Función para agregar un nuevo perfume
const agregarNuevoPerfume = () => {
  const existe = perfumesmostrar.value.some(perfume => (
    perfume.nombre === nuevoPerfume.value.nombre &&
    perfume.price === nuevoPerfume.value.price &&
    perfume.acordes === nuevoPerfume.value.acordes
  ));
  
  if (!existe) {
    // Obtener el próximo ID automáticamente
    const id = obtenerProximoId();
    // Agregar el nuevo perfume con el ID generado automáticamente
    perfumesmostrar.value.push({ ...nuevoPerfume.value, id });
    // Limpiar el formulario después de agregar
    nuevoPerfume.value = { id: 0, nombre: '', price: 0, acordes: '' };
  } else {
    alert('Por favor, complete todos los campos o su perfume ya exite en la lista. Hola Soy el alumno Luis Fernando Fuentes Kumul');
  }
};

const onSayHi = () => {
  console.log(`Se ha seleccionado un perfume`);
};
</script>

<style>

th, td {
  border: 1px solid #000000;
  padding: 8px;
}

th {
  background-color: #d000ff;
}

.Button{
    background-color: #d000ff;
}

.selected {
  background-color: rgb(21, 0, 255); 
  color: red; 
}


</style>
