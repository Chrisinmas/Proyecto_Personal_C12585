<script setup>
import { ref } from 'vue'
import AppHeader from './components/AppHeader.vue'

const modoOscuro = ref(true)
</script>

<template>
  <div :class="{ dark: modoOscuro }">
    <AppHeader :modoOscuro="modoOscuro" @toggleModo="modoOscuro = !modoOscuro" />
    <main class="contenedor">
      <RouterView />
    </main>
  </div>
</template>

<style>
:root {
  --fondo: #f2f2f5;
  --fondo-card: #ffffff;
  --texto: #111111;
  --texto-muted: #666666;
  --primario: #e23636;
  --secundario: #1a1a2e;
  --borde: #dedede;
  --sombra: rgba(0, 0, 0, 0.08);
  --header: #1a1a2e;
}

.dark {
  --fondo: #0a0a0f;
  --fondo-card: #12121e;
  --texto: #f0f0f0;
  --texto-muted: #888888;
  --primario: #e23636;
  --secundario: #1e1e35;
  --borde: #2a2a3e;
  --sombra: rgba(0, 0, 0, 0.4);
  --header: #0d0d1a;
}

*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background-color: var(--fondo);
  color: var(--texto);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  transition: background-color 0.3s, color 0.3s;
  min-height: 100vh;
}

a { text-decoration: none; color: inherit; }

.contenedor {
  max-width: 1200px;
  margin: 0 auto;
  padding: 28px 16px;
}
</style>