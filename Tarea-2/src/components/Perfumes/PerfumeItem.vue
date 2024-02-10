<template>
    <tr>
      <td>{{ perfume.id }}</td>
      <td>{{ perfume.nombre }}</td>
      <td>{{ perfume.price }}</td>
      <td>{{ perfume.acordes }}</td>
    </tr> 
  </template>
  
  <script setup lang="ts"> //Realizado por Luis Fuentes
  import type { IPerfume } from '@/interface/IPerfume';

  const perfume = defineProps<IPerfume>();
  const emits = defineEmits(['SayHi']);
  
  
  </script>
  
  <style scoped>
 
  
  td {
    padding: 8px;
  }
  
  button {
    background-color: #d000ff;
    color: #ffffff;
    border: none;
    padding: 8px 12px;
    cursor: pointer;
  }
  </style>
  