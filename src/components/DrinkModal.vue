<template>
  <div class="overlay" @click.self="$emit('close')">
    <div class="modal">
      <!-- Close button -->
      <button class="close" @click="$emit('close')">
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
import HoverCursor from '@/assets/hover.png'

defineProps({
  drink: {
    type: Object,
    required: true
  }
})

defineEmits(['close'])

const hoverCursorUrl = `url(${HoverCursor}), auto`

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
  padding: 32px;
}

.modal {
  background: #26282A;
  border-radius: 50px;
  max-width: 600px;
  width: 100%;
  padding: 32px;
  position: relative;
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.3);
}

.close {
  position: absolute;
  top: 10px;
  right: 12px;
  border: none;
  background: transparent;
  font-size: 18px;
  margin: 20px;
  cursor: v-bind(hoverCursorUrl);
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
  margin-top: 24px;
  font-size: 24px;
  font-family: "Playwrite DE SAS", cursive;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  color: white;
}

.drink-p-text {
  font-family: "Brandon Grotesque";
  src: url("BrandonGrotesque-Medium.woff2") format("woff2"),
  url("BrandonGrotesque-Medium.woff") format("woff");
  font-weight: 500;
  font-style: normal;
  color: white;
  font-size: 16px;
  margin-top: 8px;
}

ul {
  list-style: none;
  padding: 5px;
  margin: 0 auto;
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
    padding: 24px;
    border-radius: 25px;
  }

  .drink-title {
    font-size: 40px;
  }

  .drink-subtitle {
    font-size: 21px;
  }

  .drink-p-text {
    font-size: 16px;
  }
}

@media (max-width: 767px) {
  .overlay {
    align-items: flex-start;
    padding: 16px 8px;
  }

  .modal {
    width: 75%;
    max-width: none;
    max-height: 95vh;
    margin: 16px auto;
    border-radius: 20px;
    padding: 24px;
    overflow-y: auto;
  }

  .drink-title {
    font-size: 28px;
  }

  .drink-subtitle {
    font-size: 18px;
  }

  .drink-p-text {
    font-size: 14px;
  }

  ul {
    padding-left: 16px;
  }
}
</style>