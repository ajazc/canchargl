<template>
  <header class="header">
    <div class="container">
      <div class="logo-container">
        <img src="../assets/logo.png" alt="Canchas Río Gallegos" class="logo-img" />
        <h1 class="logo-text">Canchas Río Gallegos</h1>
      </div>
      <nav class="nav">
        <ul>
          <li><a href="#inicio">Inicio</a></li>
          <li><a href="#canchas">Canchas</a></li>
        </ul>
      </nav>
      <WeatherWidget />
    </div>
  </header>
</template>

<script setup>
import WeatherWidget from './WeatherWidget.vue'
</script>

<style scoped>
.header {
  background: linear-gradient(135deg, #2c3e50, #3498db);
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo-img {
  height: 50px;
  width: auto;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: bold;
  margin: 0;
}

.nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  gap: 2rem;
}

.nav a {
  color: white;
  text-decoration: none;
  font-weight: 500;
  transition: opacity 0.3s;
}

.nav a:hover {
  opacity: 0.8;
}
</style>