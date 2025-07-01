<template>
  <div>
    <h1>Lista de Películas</h1>
    <div class="container">
      <CardComponent
        v-for="pelicula in peliculas"
        :key="pelicula.id"
        :movie="pelicula"
        @update_likes="actualizarLikes"
      />
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import CardComponent from './components/CardComponent.vue';
import type { Pelicula } from './interfaces/Pelicula.ts';
import moviesData from './resources/movies';

const peliculas = ref<Pelicula[]>(moviesData);

function actualizarLikes({ id, likes }: { id: number; likes: number }) {
  const peli = peliculas.value.find(p => p.id === id);
  if (peli) {
    peli.likes = likes;
  }
}
</script>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>

