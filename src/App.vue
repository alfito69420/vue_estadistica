<template>
  <div class="grid-container">
    <div class="grid-item"><MedianaView /></div>
    <div class="grid-item"><ModaView /></div>
    <div class="grid-item"><MediaView /></div>
    <div class="grid-item"><VarianzaView /></div>
    <div class="grid-item"><DesviacionView /></div>
    <div class="grid-item"><RangoView /></div>
  </div>
</template>

<script lang="ts" setup>
import MedianaView from './views/MedianaView.vue';
import ModaView from './views/ModaView.vue';
import MediaView from './views/MediaView.vue';
import VarianzaView from './views/VarianzaView.vue';
import DesviacionView from './views/DesviacionstdView.vue';
import RangoView from './views/RangoView.vue';
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px; /* Espacio entre los elementos */
  padding: 16px; /* Espacio alrededor de la cuadrícula */
}

.grid-item {
  background-color: #f9f9f9; /* Color de fondo para distinguir cada módulo */
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>