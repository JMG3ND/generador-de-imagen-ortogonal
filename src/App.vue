<template>
  <h1>Generador de Imágen Ortogonal</h1>
  <div class="image-container">
    <OrtogonalCube :image="image" />
  </div>
</template>

<script setup>
import OrtogonalCube from './components/OrtogonalCube.vue';

//Contenido de las secciones
//null = 0 white = 1, orange = 2, blue = 3, red = 4, green = 5, yellow = 6
const n = 0, w = 1, o = 2, b = 3, r = 4, g = 5, y = 6;
const image = {
  up: [n, n, n, b, y, n, b, n, n],
  left: [o, o, n, n, o, o, n, o, o],
  right: [w, n, n, n, b, b, n, b, b]
}
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