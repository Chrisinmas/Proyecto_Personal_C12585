<script setup>
const props = defineProps({ modoOscuro: Boolean })
const emit = defineEmits(['toggleModo'])
</script>

<template>
  <header class="header">
    <div class="header-inner">
      <RouterLink to="/" class="logo">
        <span class="logo-m">M</span>
        <span class="logo-rest">arvel</span>
        <span class="logo-pedia">Pedia</span>
      </RouterLink>
      <button class="btn-modo" @click="emit('toggleModo')" :title="modoOscuro ? 'Modo claro' : 'Modo oscuro'">
        {{ modoOscuro ? '☀️' : '🌙' }}
      </button>
    </div>
  </header>
</template>

<style scoped>
.header {
  background-color: var(--header);
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 12px rgba(0,0,0,0.5);
}

.header-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 14px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  font-size: 1.6rem;
  font-weight: 900;
  letter-spacing: 1px;
  color: #ffffff;
}

.logo-m {
  color: var(--primario);
  font-size: 2rem;
}

.logo-rest { color: #ffffff; }

.logo-pedia {
  color: var(--primario);
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 3px;
  vertical-align: super;
}

.btn-modo {
  background: none;
  border: 2px solid rgba(255,255,255,0.2);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  cursor: pointer;
  font-size: 1.1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.2s;
}

.btn-modo:hover { border-color: var(--primario); }
</style>