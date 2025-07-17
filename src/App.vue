<script>
import ArithmeticSequence from './components/ArithmeticSequence.vue'
import GeometricSequence from './components/GeometricSequence.vue'

export default {
  name: 'App',
  components: {
    ArithmeticSequence,
    GeometricSequence
  },
  data() {
    return {
      currentView: 'arithmetic'
    }
  },
  methods: {
    switchView(view) {
      this.currentView = view;
    }
  }
}
</script>

<template>
  <div class="app">
    <nav class="nav">
      <a 
        href="#" 
        :class="{ active: currentView === 'arithmetic' }" 
        @click.prevent="switchView('arithmetic')"
      >
        Arithmetic Sequence
      </a>
      <a 
        href="#" 
        :class="{ active: currentView === 'geometric' }" 
        @click.prevent="switchView('geometric')"
      >
        Geometric Sequence
      </a>
    </nav>
    
    <ArithmeticSequence v-if="currentView === 'arithmetic'" />
    <GeometricSequence v-if="currentView === 'geometric'" />
  </div>
</template>

<style>
body {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f5f5f5;
}

.app {
  width: 100%;
}

.nav {
  background-color: #4CAF50;
  padding: 10px 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  display: flex;
  gap: 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.nav a {
  color: white;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 4px;
  transition: background-color 0.3s;
  opacity: 0.9;
  cursor: pointer;
}

.nav a:hover {
  background-color: #45a049;
  opacity: 1;
}

.nav a.active {
  background-color: #45a049;
  font-weight: bold;
  opacity: 1;
}
</style>
