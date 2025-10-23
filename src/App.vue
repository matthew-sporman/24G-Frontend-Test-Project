<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
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
}

/* Tablet view: 768px–1024px */
@media (min-width: 768px) and (max-width: 1024px) {
  #app {
    background-image: url('https://assets.24g.com/public/2022-frontend-test-project/bg_tablet.png');
    padding: 1.5rem;
  }

  .the-24G-logo {
    height: 60px;
    margin: 20px auto;
  }

  .welcome-message {
    font-size: 50px;
    margin: 20px;
  }

  .cards {
    gap: 1rem;
  }

  .drink-card {
    width: 200px;
  }
}

/* Mobile view: up to 767px */
@media (max-width: 767px) {
  #app {
    background-image: url('https://assets.24g.com/public/2022-frontend-test-project/bg_mobile.png');
    padding: 1rem;
  }

  .the-24G-logo {
    height: 50px;
    margin: 15px auto;
  }

  .welcome-message {
    font-size: 28px;
    margin: 10px;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.6);
  }

  .cards {
    flex-direction: column;
    align-items: center;
    gap: 0.75rem;
  }

  .drink-card {
    width: 90%;
    max-width: 300px;
    padding: 0.75rem;
  }
}
</style>