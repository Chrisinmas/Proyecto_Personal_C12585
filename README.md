# MarvelPedia — Enciclopedia Interactiva del Universo Marvel

Proyecto Personal del curso IF7102 Multimedios | I Ciclo 2026
Universidad de Costa Rica — Sede Regional de Guanacaste
Estudiante: Christopher Duarte | Carnet: C12585

---

## Descripción

MarvelPedia es una enciclopedia web interactiva de personajes del Universo Marvel, construida con **Vue 3** como framework principal. Permite explorar 10 personajes icónicos con información detallada, búsqueda en tiempo real, filtros por categoría, modo oscuro/claro y narración en audio para personajes seleccionados.

---

## Framework utilizado

**Vue 3** con Vite — Composition API (`<script setup>`)

---

## Funcionalidades

- Búsqueda en tiempo real por nombre o nombre real
- Filtros por categoría: Vengadores, X-Men, Villanos, Guardianes
- Vista de detalle por personaje con imagen, descripción, poderes y datos
- Reproductor de audio con narración propia para 3 personajes
- Modo oscuro y claro con toggle
- Diseño responsivo para escritorio y móvil
- Datos cargados dinámicamente desde archivo JSON

---

## Tecnologías

- Vue 3 (Composition API)
- Vue Router
- Vite
- CSS Variables
- HTML5 Audio API

---

## Estructura del proyecto

```
src/
├── components/
│   ├── AppHeader.vue
│   ├── EntradaCard.vue
│   ├── FiltrosCategorias.vue
│   └── AudioPlayer.vue
├── views/
│   ├── HomeView.vue
│   └── DetalleView.vue
├── router/
│   └── index.js
├── App.vue
└── main.js
public/
├── data/
│   └── personajes.json
├── images/
└── audio/
```

---

## Instrucciones de ejecución

### Requisitos
- Node.js v18 o superior
- npm

### Pasos

1. Clonar el repositorio:
```bash
git clone https://github.com/Chrisinmas/Proyecto_Personal_C12585.git
```

2. Entrar a la carpeta:
```bash
cd Proyecto_Personal_C12585
```

3. Instalar dependencias:
```bash
npm install
```

4. Correr en modo desarrollo:
```bash
npm run dev
```

5. Abrir en el navegador:
```
http://localhost:5173
```

---

## Capturas de pantalla

### Vista principal — Modo oscuro
![Vista principal modo oscuro](capturas/home-oscuro.png)

### Vista principal — Modo claro
![Vista principal modo claro](capturas/home-claro.png)

### Vista de detalle
![Vista de detalle](capturas/detalle.png)

---

## Licencia

Proyecto académico — Universidad de Costa Rica | IF7102 Multimedios | I Ciclo 2026