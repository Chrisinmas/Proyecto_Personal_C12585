<script setup>
import { ref, computed, onMounted } from 'vue'
import EntradaCard from '../components/EntradaCard.vue'
import FiltrosCategorias from '../components/FiltrosCategorias.vue'

const personajes = ref([])
const busqueda = ref('')
const categoriaActiva = ref('Todos')

const categorias = computed(() => {
  const unicas = new Set()
  personajes.value.forEach(p => p.categorias.forEach(c => unicas.add(c)))
  return ['Todos', ...unicas]
})

const personajesFiltrados = computed(() => {
  return personajes.value.filter(p => {
    const texto = busqueda.value.toLowerCase()
    const coincideBusqueda =
      p.nombre.toLowerCase().includes(texto) ||
      p.nombreReal.toLowerCase().includes(texto)
    const coincideCategoria =
      categoriaActiva.value === 'Todos' || p.categorias.includes(categoriaActiva.value)
    return coincideBusqueda && coincideCategoria
  })
})

onMounted(async () => {
  const res = await fetch('/data/personajes.json')
  personajes.value = await res.json()
})
</script>

<template>
  <div>
    <section class="hero">
      <p class="hero-eyebrow">Universo Marvel</p>
      <h1 class="hero-titulo">MARVELPEDIA</h1>
      <p class="hero-sub">Enciclopedia interactiva de personajes del Universo Marvel</p>
      <input
        v-model="busqueda"
        class="buscador"
        type="text"
        placeholder="🔍  Buscar por nombre o nombre real..."
      />
    </section>

    <FiltrosCategorias
      :categorias="categorias"
      :categoriaActiva="categoriaActiva"
      @cambiarCategoria="cat => categoriaActiva = cat"
    />

    <p class="contador" v-if="personajes.length > 0">
      {{ personajesFiltrados.length }}
      {{ personajesFiltrados.length === 1 ? 'personaje encontrado' : 'personajes encontrados' }}
    </p>

    <div v-if="personajes.length === 0" class="estado">Cargando personajes...</div>

    <div v-else-if="personajesFiltrados.length === 0" class="estado">
      No se encontraron resultados para "<strong>{{ busqueda }}</strong>"
    </div>

    <div v-else class="grilla">
      <EntradaCard
  v-for="p in personajesFiltrados"
  :key="p.id"
  :personaje="p"
  :categoriaActiva="categoriaActiva"
/>
    </div>
  </div>
</template>

<style scoped>
.hero {
  text-align: center;
  padding: 52px 16px 36px;
  margin-bottom: 8px;
}

.hero-eyebrow {
  font-size: 0.85rem;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--primario);
  margin-bottom: 8px;
}

.hero-titulo {
  font-size: clamp(2.5rem, 8vw, 5rem);
  font-weight: 900;
  color: var(--texto);
  letter-spacing: 6px;
  line-height: 1;
  margin-bottom: 14px;
}

.hero-sub {
  font-size: 1rem;
  color: var(--texto-muted);
  margin-bottom: 28px;
}

.buscador {
  width: 100%;
  max-width: 520px;
  padding: 13px 22px;
  border-radius: 30px;
  border: 2px solid var(--borde);
  background-color: var(--fondo-card);
  color: var(--texto);
  font-size: 0.95rem;
  outline: none;
  transition: border-color 0.2s;
}

.buscador:focus { border-color: var(--primario); }

.contador {
  font-size: 0.85rem;
  color: var(--texto-muted);
  margin-bottom: 20px;
}

.grilla {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 24px;
}

.estado {
  text-align: center;
  padding: 80px 20px;
  color: var(--texto-muted);
  font-size: 1.05rem;
}
</style>