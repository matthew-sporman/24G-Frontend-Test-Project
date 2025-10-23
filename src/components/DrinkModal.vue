<template>
  <!-- Overlay covers entire screen -->
  <div class="overlay" @click.self="$emit('close')">
    <div class="modal">
      <!-- Close button -->
      <button class="close" @click="$emit('close')"
  >
  <img :src="CloseIcon" alt="Close" width="24" height="24" />
      </button>

      <h2 class = "drink-title">{{ drink.name }}</h2>

      <p class = "drink-p-text" v-if="drink.glassware"><strong>Glassware:</strong> {{ drink.glassware }}</p>

      <p class = "drink-p-text" v-if="drink.mocktail"><strong>Mocktail:</strong> {{ drink.mocktail }}</p>

      <h3 class="drink-subtitle">Ingredients</h3>
      <ul>
        <li v-for="(item, index) in drink.ingredients" :key="index">{{ item }}</li>
      </ul>

      <h3 class = "drink-subtitle">Steps</h3>
      <ul>
        <li v-for="(step, index) in drink.steps" :key="index">{{ step }}</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'
import CloseIcon from '@/assets/close.svg'
import ArrowCursor from '@/assets/arrowhead-rounded-outline.png'

defineProps({
  drink: {
    type: Object,
    required: true
  }
})

defineEmits(['close'])

// Prevents background scroll when modal is open on mobile and tablet
onMounted(() => {
  document.body.style.overflow = 'hidden'
})

onUnmounted(() => {
  document.body.style.overflow = ''
  document.body.style.cursor = `url(${ArrowCursor}), auto`
})
</script>

<style scoped>
/* Google Font import for Drink details */
@import url('https://fonts.googleapis.com/css2?family=Playwrite+DE+SAS:wght@100..400&display=swap');

/* Full-screen overlay */
.overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  overflow-y: auto;
  padding: 2rem;
}

.modal {
  background: #26282A;
  border-radius: 50px;
  max-width: 600px;
  width: 100%;
  padding: 2rem;
  position: relative;
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.3);
}

.close {
  position: absolute;
  top: 10px;
  right: 12px;
  border: none;
  background: transparent;
  font-size: 1.2rem;
  margin: 20px;
  cursor: url('@/hover.png'), auto;
}

.close:hover {
  cursor: url('@/hover.png'), auto;
}

.close img {
  /* makes the close icon white */
  filter: invert(100%);
}

.drink-title {
  font-family: "Writable Story";
  src: url("Writable-Story.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
  font-size: 50px;
  color: white
}

.drink-subtitle {
  margin-top: 1.5rem;
  font-size: 1.5rem;
  font-family: "Playwrite DE SAS", cursive;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  color: white;
}

.drink-p-text {
  font-family: "Playwrite DE SAS", cursive;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  color: white;
  font-size: 1rem;
  margin-top: 0.5rem;
}

ul {
  padding-left: 1.5rem;
  margin: 0.5rem 0 1rem 0;
  color: white;
  font-family: "Brandon Grotesque";
  src: url("BrandonGrotesque-Medium.woff2") format("woff2"),
  url("BrandonGrotesque-Medium.woff") format("woff");
  font-weight: 500;
  font-style: normal;
}

@media (min-width: 768px) and (max-width: 1024px) {
  .modal {
    max-width: 500px;
    padding: 1.5rem;
    border-radius: 25px;
  }

  .drink-title {
    font-size: 40px;
  }

  .drink-subtitle {
    font-size: 1.3rem;
  }

  .drink-p-text {
    font-size: 0.95rem;
  }
}

@media (max-width: 767px) {
  .overlay {
    align-items: flex-start;
    padding: 1rem 0.5rem;
  }

  .modal {
    width: 75%;
    max-width: none;
    max-height: 95vh;
    margin: 1rem auto;
    border-radius: 20px;
    padding: 1.25rem;
    overflow-y: auto;
  }

  .drink-title {
    font-size: 28px;
  }

  .drink-subtitle {
    font-size: 1.1rem;
  }

  .drink-p-text {
    font-size: 0.9rem;
  }

  ul {
    padding-left: 1rem;
  }
}
</style>