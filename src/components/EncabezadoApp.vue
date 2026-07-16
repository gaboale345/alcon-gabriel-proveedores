<script setup>
const props = defineProps({
  titulo: {
    type: String,
    required: true,
  },
  subtitulo: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <header class="encabezado-app">
    <h1>{{ props.titulo }}</h1>
    <p>{{ props.subtitulo }}</p>
  </header>
</template>

<style scoped>
.encabezado-app {
  max-width: 1100px;
  margin: 0 auto 2rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid #dbeafe;
}

.encabezado-app h1 {
  margin: 0 0 0.4rem;
  font-size: 2rem;
  color: #1e3a8a;
}

.encabezado-app p {
  margin: 0;
  color: #4b5563;
  font-size: 1rem;
}
</style>
