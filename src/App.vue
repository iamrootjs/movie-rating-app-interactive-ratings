<script setup>
import { reactive } from "vue";
import { StarIcon as SolidStarIcon } from "@heroicons/vue/24/solid";
import { StarIcon as OutlineStarIcon } from "@heroicons/vue/24/outline";
import { items } from "./movies.json";
const movies = reactive(items);
</script>

<template>
  <div class="app">
    <div class="movie-list">
      <div class="movie-item" v-for="movie in movies" :key="movie.id">
        <div class="movie-item-image-wrapper">
          <img :src="movie.image" class="movie-item-image" alt="" />
        </div>

        <div class="movie-item-content-wrapper">
          <div class="movie-item-title-wrapper">
            <h3 class="movie-item-title">{{ movie.name }}</h3>
            <div class="movie-item-genres-wrapper">
              <span
                v-for="genre in movie.genres"
                :key="`${movie.id}-${genre}`"
                class="movie-item-genre-tag"
                >{{ genre }}</span
              >
            </div>
          </div>
          <div class="movie-item-description-wrapper">
            <p class="movie-item-description">{{ movie.description }}</p>
          </div>
          <div class="movie-item-rating-wrapper">
            <span class="movie-item-rating-text">
              Rating: ({{ movie.rating }}/5)
            </span>
            <template>
              <button
                class="flex"
                @click="updateRating(index + 1)"
                v-for="(star, index) in 5"
                :key="index"
                :disabled="rating === index + 1"
              >
                <SolidStarIcon class="movie-item-star-icon" v-if="index < rating" />
                <OutlineStarIcon class="movie-item-star-icon" v-else />
              </button>
            </template>

            <script setup>
            import { defineProps } from 'vue'
            import { StarIcon as SolidStarIcon } from "@heroicons/vue/24/solid";
            import { StarIcon as OutlineStarIcon } from "@heroicons/vue/24/outline";

            const props = defineProps({
              rating: {
                type: Number,
                required: true
              },
              updateRating: {
                type: Function,
                required: true
              }
            })
            </script>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
