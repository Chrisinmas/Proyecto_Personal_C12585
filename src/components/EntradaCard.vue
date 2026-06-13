<script setup>
import { useRouter } from 'vue-router'

const props = defineProps({ personaje: Object, categoriaActiva: String })
const router = useRouter()

function verDetalle() {
  router.push(`/personaje/${props.personaje.id}`)
}
</script>

<template>
  <div class="card" @click="verDetalle">
    <div class="card-img-wrap">
      <img
        :src="personaje.imagen"
        :alt="personaje.nombre"
        class="card-img"
        @error="$event.target.src = `https://placehold.co/300x350/1a1a2e/e23636?text=${personaje.nombre}`"
      />
      <span class="badge-cat">{{ categoriaActiva !== 'Todos' && personaje.categorias.includes(categoriaActiva) ? categoriaActiva : personaje.categorias[0] }}</span>
      <div v-if="personaje.audio" class="badge-audio">🎧</div>
    </div>
    <div class="card-body">
      <h3 class="card-nombre">{{ personaje.nombre }}</h3>
      <p class="card-nombre-real">{{ personaje.nombreReal }}</p>
      <p class="card-desc">{{ personaje.descripcion }}</p>
      <div class="card-categorias" v-if="personaje.categorias.length > 1">
        <span v-for="cat in personaje.categorias" :key="cat" class="tag-cat">{{ cat }}</span>
      </div>
      <div class="card-poderes">
        <span v-for="poder in personaje.poderes.slice(0, 2)" :key="poder" class="tag-poder">
          {{ poder }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  background-color: var(--fondo-card);
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  border: 1px solid var(--borde);
  box-shadow: 0 4px 12px var(--sombra);
  transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 28px var(--sombra);
  border-color: var(--primario);
}

.card-img-wrap {
  position: relative;
  height: 220px;
  overflow: hidden;
  background-color: var(--secundario);
}

.card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
  transition: transform 0.3s;
}

.card:hover .card-img { transform: scale(1.05); }

.badge-cat {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: var(--primario);
  color: #fff;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.badge-audio {
  position: absolute;
  bottom: 10px;
  left: 10px;
  background-color: rgba(0,0,0,0.6);
  padding: 4px 8px;
  border-radius: 8px;
  font-size: 0.85rem;
}

.card-body { padding: 16px; }

.card-nombre {
  font-size: 1.1rem;
  font-weight: 800;
  margin-bottom: 2px;
}

.card-nombre-real {
  font-size: 0.82rem;
  color: var(--primario);
  font-weight: 600;
  margin-bottom: 10px;
}

.card-desc {
  font-size: 0.83rem;
  color: var(--texto-muted);
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  margin-bottom: 10px;
}

.card-categorias {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-bottom: 8px;
}

.tag-cat {
  background-color: var(--primario);
  color: #fff;
  padding: 2px 8px;
  border-radius: 6px;
  font-size: 0.7rem;
  font-weight: 600;
}

.card-poderes { display: flex; gap: 6px; flex-wrap: wrap; }

.tag-poder {
  background-color: var(--secundario);
  border: 1px solid var(--borde);
  color: var(--texto);
  padding: 3px 8px;
  border-radius: 6px;
  font-size: 0.72rem;
}
</style>