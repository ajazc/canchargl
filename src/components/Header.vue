<template>
  <header class="bg-gradient-to-br from-[#2c3e50] to-[#3498db] text-white py-4 shadow-lg">
    <div class="max-w-[1200px] mx-auto px-8 flex justify-between items-center">
      <div class="flex items-center gap-4">
        <img src="../assets/logo.png" alt="Canchas Río Gallegos" class="h-[50px] w-auto" />
        <h1 class="text-2xl font-bold m-0">Canchas Río Gallegos</h1>
      </div>
      <nav>
        <ul class="list-none m-0 p-0 flex gap-8">
          <li><a href="#inicio" class="text-white no-underline font-medium transition-opacity duration-300 hover:opacity-80">Inicio</a></li>
        </ul>
      </nav>
      <WeatherWidget />
    </div>
  </header>
</template>

<script setup>
import WeatherWidget from './WeatherWidget.vue'
</script>
