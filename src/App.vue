<script setup>
import { ref, onMounted } from 'vue'
import DrinkInfoCard from './components/DrinkInfoCard.vue'
import DrinkModal from './components/DrinkModal.vue'

const drinks = ref([])
const selectedDrink = ref(null)

// Load drinks from JSON
onMounted(async () => {
    try {
    const res = await fetch('https://assets.24g.com/public/2022-frontend-test-project/drinks.json')
    const data = await res.json()
    drinks.value = data.drinks || []
    console.log('Loaded drinks:', drinks.value)
  } catch (err) {
    console.error('Failed to load drinks:', err)
  }
})

// Open modal with clicked drink
function openModal(drink) {
  selectedDrink.value = drink
}

// Close modal
function closeModal() {
  selectedDrink.value = null
}
</script>

<template>
 <div id="app" class="background">
    <header>
      <img
        src="https://assets.24g.com/public/2022-frontend-test-project/24g_logo.svg"
        class="the-24G-logo"
      />
    </header>
    <h2 class="welcome-message">Welcome! Drinks below are the Team's favorites! Select one to learn more!</h2>

    <!-- Main content slot -->
    <main>
      <div class="cards">
        <!-- Render the drink cards -->
        <DrinkInfoCard
          v-for="drink in drinks"
          :key="drink.id"
          :drink="drink"
    @open="openModal"
        />
      </div>

      <!-- Modal -->
      <DrinkModal
        v-if="selectedDrink"
        :drink="selectedDrink"
        @close="closeModal"
      />
    </main>
  </div>
</template>

<style scoped>
/* URL below hosts required fonts */
@import url('https://assets.24g.com/public/2022-frontend-test-project/fonts.css');
#app {
  background-image: url('https://assets.24g.com/public/2022-frontend-test-project/bg_desktop.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  text-align: center;
  padding: 2rem;
  cursor: url(public/arrowhead-rounded-outline.svg) 12 12, auto;
}

.the-24G-logo {
  margin: 25px;
  padding: 20px;
  height: 75px;
}

.welcome-message {
  font-family: "Writable Story";
  src: url("Writable-Story.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
  color: white;
  font-size: 75px;
  text-align: center;
  margin: 25px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.5rem;
}

.drink-card {
  border: 2.5px solid white;
  border-radius: 25px;
  cursor: url(public/hover.svg) 12 12, auto;
}
</style>