<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import AudioPlayer from '../components/AudioPlayer.vue'

const route = useRoute()
const router = useRouter()
const personaje = ref(null)

onMounted(async () => {
  const res = await fetch('/data/personajes.json')
  const data = await res.json()
  personaje.value = data.find(p => p.id === parseInt(route.params.id)) || null
})
</script>

<template>
  <div>
    <button class="btn-volver" @click="router.push('/')">← Volver</button>

    <div v-if="!personaje" class="cargando">Cargando...</div>

    <article v-else class="detalle">
      <div class="col-imagen">
        <img
          :src="personaje.imagen"
          :alt="personaje.nombre"
          class="detalle-img"
          @error="$event.target.src = `https://placehold.co/400x500/1a1a2e/e23636?text=${personaje.nombre}`"
        />
        <span class="detalle-cat">{{ personaje.categoria }}</span>
        <AudioPlayer v-if="personaje.audio" :src="personaje.audio" :nombre="personaje.nombre" />
      </div>

      <div class="col-info">
        <h1 class="detalle-nombre">{{ personaje.nombre }}</h1>
        <p class="detalle-nombre-real">{{ personaje.nombreReal }}</p>
        <p class="detalle-desc">{{ personaje.descripcionLarga }}</p>

        <div class="detalle-dato">
          <span class="dato-label">Primera aparición</span>
          <span>{{ personaje.primerAparicion }}</span>
        </div>
        <div class="detalle-dato">
          <span class="dato-label">Creadores</span>
          <span>{{ personaje.creadores }}</span>
        </div>

        <div class="poderes-seccion">
          <span class="dato-label">Poderes y habilidades</span>
          <div class="poderes-lista">
            <span v-for="poder in personaje.poderes" :key="poder" class="poder-badge">
              {{ poder }}
            </span>
          </div>
        </div>
      </div>
    </article>
  </div>
</template>

<style scoped>
.btn-volver {
  background: none;
  border: 2px solid var(--borde);
  color: var(--texto);
  padding: 8px 18px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9rem;
  margin-bottom: 28px;
  transition: all 0.2s;
}

.btn-volver:hover { border-color: var(--primario); color: var(--primario); }

.detalle {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 48px;
  align-items: start;
}

.detalle-img {
  width: 100%;
  border-radius: 12px;
  object-fit: cover;
  object-position: top;
  max-height: 420px;
  border: 2px solid var(--borde);
}

.detalle-cat {
  display: inline-block;
  background-color: var(--primario);
  color: #fff;
  padding: 5px 14px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 700;
  margin-top: 12px;
  letter-spacing: 1px;
}

.detalle-nombre {
  font-size: 2.4rem;
  font-weight: 900;
  letter-spacing: 1px;
  margin-bottom: 6px;
  line-height: 1.1;
}

.detalle-nombre-real {
  font-size: 1.05rem;
  color: var(--primario);
  font-weight: 600;
  margin-bottom: 20px;
}

.detalle-desc {
  font-size: 0.97rem;
  line-height: 1.75;
  color: var(--texto-muted);
  margin-bottom: 24px;
}

.detalle-dato {
  margin-bottom: 14px;
  font-size: 0.92rem;
}

.dato-label {
  display: block;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--primario);
  margin-bottom: 4px;
}

.poderes-seccion { margin-top: 20px; }

.poderes-lista {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 10px;
}

.poder-badge {
  background-color: var(--primario);
  color: #fff;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.82rem;
  font-weight: 600;
}

.cargando {
  text-align: center;
  padding: 80px;
  color: var(--texto-muted);
}

@media (max-width: 768px) {
  .detalle { grid-template-columns: 1fr; }
}
</style>