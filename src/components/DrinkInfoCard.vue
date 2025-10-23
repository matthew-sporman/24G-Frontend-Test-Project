<template>
  <div
    class="drink-card"
    @click="$emit('open', drink)"
    @mouseenter="hovered = true"
    @mouseleave="hovered = false"
  >
    <!-- Image flips on hover (requirement!) -->
    <img
    :src="hovered ? drink.images?.back : drink.images?.front"
    :alt="drink.name"
    class="card-image"
/>
    
    <h3 class="drink-name">{{ drink.name }}</h3>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import HoverCursor from '@/assets/hover.png'

defineProps({
  drink: { type: Object, required: true }
})

defineEmits(['open'])

const hovered = ref(false)

const hoverCursorUrl = `url(${HoverCursor}), auto`
</script>

<style scoped>
.drink-card {
  width: 200px;
  text-align: center;
  transition: transform 0.2s ease;
  border: 2px solid #353E43;
  border-radius: 25px;
  background-color: rgba(0,0,0,0.3);
  padding: 0.5rem;
}

.drink-card:hover {
  transform: scale(1.05);
  cursor: v-bind(hoverCursorUrl);
}

.card-image {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
  display: block;
  margin-bottom: 0.5rem;
}

.drink-name {
  font-family: 'Brandon Grotesque', sans-serif;
  font-weight: 500;
  font-size: 1rem;
  color: #fff;
  margin: 0;
}
</style>