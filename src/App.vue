<template>
  <h1>Generador de Imágen Ortogonal</h1>
  <div class="image-container">
    <OrtogonalCube :image="image" />
  </div>
</template>

<script setup>
import OrtogonalCube from './components/OrtogonalCube.vue';
</script>

<style>
h1 {
  text-align: center;
}

.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 600px;
  height: 600px;
}
</style>