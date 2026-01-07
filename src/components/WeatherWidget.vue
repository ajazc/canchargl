<template>
  <div class="bg-white/20 px-4 py-2 rounded-xl backdrop-blur-sm text-white text-sm border border-white/10 transition-all duration-300 ease-in-out hover:bg-white/30" v-if="weather">
    <div class="flex items-center gap-3">
      <span class="text-[1.8rem]">{{ weatherCondition.icon }}</span>
      <div class="flex flex-col">
        <span class="text-xs opacity-90 uppercase tracking-wide font-semibold">Río Gallegos</span>
        <div class="flex items-center gap-2">
          <span class="text-lg font-bold">{{ Math.round(weather.temperature) }}°C</span>
          <span class="text-sm opacity-90 pl-2 border-l border-white/40">{{ weatherCondition.label }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const weather = ref(null)

const getWeatherCondition = (code, windspeed) => {
  // Check for high wind first (Rio Gallegos is known for wind)
  // Threshold: 40 km/h for "Ventoso" override or addition? 
  // Let's make it a distinct state if it's really windy and not raining hard.
  const isWindy = windspeed > 40;

  // WMO Weather interpretation codes (WW)
  // 0: Clear sky
  // 1, 2, 3: Mainly clear, partly cloudy, and overcast
  // 45, 48: Fog
  // 51, 53, 55, 56, 57: Drizzle
  // 61, 63, 65, 66, 67: Rain
  // 71, 73, 75, 77: Snow
  // 80, 81, 82: Rain showers
  // 85, 86: Snow showers
  // 95, 96, 99: Thunderstorm

  if (code >= 95) return { label: 'Tormenta', icon: '⚡' };
  if (code >= 71) return { label: 'Nevando', icon: '❄️' };
  if (code >= 51 || (code >= 80 && code <= 82)) return { label: 'Lloviendo', icon: '🌧️' };
  if (code >= 45 && code <= 48) return { label: 'Niebla', icon: '🌫️' };
  
  if (isWindy) return { label: 'Ventoso', icon: '💨' };

  if (code === 0) return { label: 'Soleado', icon: '☀️' };
  if (code <= 3) return { label: 'Nublado', icon: '☁️' };

  return { label: 'Despejado', icon: '☀️' };
}

const weatherCondition = computed(() => {
  if (!weather.value) return { label: '', icon: '' };
  return getWeatherCondition(weather.value.weathercode, weather.value.windspeed);
})

const fetchWeather = async () => {
  try {
    const response = await fetch(
      'https://api.open-meteo.com/v1/forecast?latitude=-51.6226&longitude=-69.2181&current_weather=true'
    )
    const data = await response.json()
    weather.value = data.current_weather
  } catch (error) {
    console.error('Error fetching weather:', error)
  }
}

onMounted(() => {
  fetchWeather()
  setInterval(fetchWeather, 30 * 60 * 1000)
})
</script>


