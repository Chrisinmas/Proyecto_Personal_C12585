<script setup>
defineProps({ categorias: Array, categoriaActiva: String })
const emit = defineEmits(['cambiarCategoria'])
</script>

<template>
  <div class="filtros">
    <button
      v-for="cat in categorias"
      :key="cat"
      :class="['btn-filtro', { activo: cat === categoriaActiva }]"
      @click="emit('cambiarCategoria', cat)"
    >
      {{ cat }}
    </button>
  </div>
</template>

<style scoped>
.filtros {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 28px;
}

.btn-filtro {
  padding: 8px 20px;
  border-radius: 20px;
  border: 2px solid var(--primario);
  background: transparent;
  color: var(--primario);
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 600;
  transition: all 0.2s;
}

.btn-filtro:hover,
.btn-filtro.activo {
  background-color: var(--primario);
  color: #ffffff;
}
</style>