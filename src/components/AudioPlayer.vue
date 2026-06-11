<script setup>
import { ref, watch } from 'vue'

const props = defineProps({ src: String, nombre: String })

const audio = ref(null)
const reproduciendo = ref(false)
const progreso = ref(0)
const tiempoActual = ref('0:00')
const tiempoTotal = ref('0:00')

function togglePlay() {
  if (!audio.value) return
  if (reproduciendo.value) {
    audio.value.pause()
    reproduciendo.value = false
  } else {
    audio.value.play()
    reproduciendo.value = true
  }
}

function actualizarProgreso() {
  if (!audio.value) return
  progreso.value = (audio.value.currentTime / audio.value.duration) * 100 || 0
  tiempoActual.value = formatear(audio.value.currentTime)
}

function cargarDuracion() {
  if (!audio.value) return
  tiempoTotal.value = formatear(audio.value.duration)
}

function alTerminar() {
  reproduciendo.value = false
  progreso.value = 0
  tiempoActual.value = '0:00'
}

function formatear(seg) {
  if (!seg || isNaN(seg)) return '0:00'
  const m = Math.floor(seg / 60)
  const s = Math.floor(seg % 60).toString().padStart(2, '0')
  return `${m}:${s}`
}

watch(() => props.src, () => {
  reproduciendo.value = false
  progreso.value = 0
  tiempoActual.value = '0:00'
})
</script>

<template>
  <div class="player" v-if="src">
    <audio
      ref="audio"
      :src="src"
      @timeupdate="actualizarProgreso"
      @loadedmetadata="cargarDuracion"
      @ended="alTerminar"
    ></audio>
    <div class="player-body">
      <button class="btn-play" @click="togglePlay">
        {{ reproduciendo ? '⏸' : '▶' }}
      </button>
      <div class="player-info">
        <span class="player-label">🎧 Narración: {{ nombre }}</span>
        <div class="barra">
          <div class="barra-fill" :style="{ width: progreso + '%' }"></div>
        </div>
        <span class="player-tiempo">{{ tiempoActual }} / {{ tiempoTotal }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.player {
  background-color: var(--secundario);
  border: 1px solid var(--borde);
  border-radius: 10px;
  padding: 14px;
  margin-top: 20px;
}

.player-body {
  display: flex;
  align-items: center;
  gap: 14px;
}

.btn-play {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  border: none;
  background-color: var(--primario);
  color: #fff;
  font-size: 1rem;
  cursor: pointer;
  flex-shrink: 0;
  transition: background-color 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-play:hover { background-color: #c0392b; }

.player-info { flex: 1; }

.player-label {
  display: block;
  font-size: 0.78rem;
  color: var(--texto-muted);
  margin-bottom: 6px;
}

.barra {
  width: 100%;
  height: 4px;
  background-color: var(--borde);
  border-radius: 2px;
  overflow: hidden;
  margin-bottom: 4px;
}

.barra-fill {
  height: 100%;
  background-color: var(--primario);
  transition: width 0.2s linear;
}

.player-tiempo {
  font-size: 0.72rem;
  color: var(--texto-muted);
}
</style>