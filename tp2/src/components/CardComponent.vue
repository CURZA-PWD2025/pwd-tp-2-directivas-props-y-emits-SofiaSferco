<template>
  <div class="card">
    <h2>{{ movie.titulo }}</h2>
    <p><strong>Género:</strong> {{ movie.genero }}</p>
    <p><strong>Director:</strong> {{ movie.director }}</p>
    <p><strong>Año:</strong> {{ movie.anio }}</p>

    <div v-if="movie.portada">
      <img :src="movie.portada" alt="Portada" class="portada" />
    </div>
    <div v-else>
      <p>Portada no disponible</p>
    </div>

    <button @click="toggleLike">
      {{ liked ? "Quitar Like" : "Me gusta" }}
    </button>

    <p v-show="movie.likes > 0">Likes: {{ movie.likes }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Pelicula } from '../interfaces/pelicula';

const props = defineProps<{ movie: Pelicula }>();
const emit = defineEmits<{
  (e: 'update_likes', payload: { id: number; likes: number }): void;
}>();

const liked = ref(false);

function toggleLike() {
  liked.value = !liked.value;
  const newLikes = liked.value ? props.movie.likes + 1 : props.movie.likes - 1;
  emit('update_likes', { id: props.movie.id, likes: newLikes });
}
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin: 1rem;
  border-radius: 10px;
  width: 300px;
}
.portada {
  width: 100%;
  border-radius: 8px;
  margin-top: 0.5rem;
}
</style>
