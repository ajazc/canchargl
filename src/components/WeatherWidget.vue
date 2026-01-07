<template>
  <div class="weather-widget" v-if="weather">
    <div class="weather-content">
      <span class="weather-icon">{{ weatherCondition.icon }}</span>
      <div class="weather-info">
        <span class="location">Río Gallegos</span>
        <div class="temp-row">
          <span class="temperature">{{ Math.round(weather.temperature) }}°C</span>
          <span class="condition">{{ weatherCondition.label }}</span>
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

<style scoped>
.weather-widget {
  background: rgba(255, 255, 255, 0.2);
  padding: 0.5rem 1rem;
  border-radius: 12px;
  backdrop-filter: blur(5px);
  color: white;
  font-size: 0.9rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.weather-widget:hover {
  background: rgba(255, 255, 255, 0.3);
}

.weather-content {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.weather-icon {
  font-size: 1.8rem;
}

.weather-info {
  display: flex;
  flex-direction: column;
}

.location {
  font-size: 0.75rem;
  opacity: 0.9;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  font-weight: 600;
}

.temp-row {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.temperature {
  font-size: 1.1rem;
  font-weight: bold;
}

.condition {
  font-size: 0.9rem;
  opacity: 0.9;
  padding-left: 0.5rem;
  border-left: 1px solid rgba(255,255,255,0.4);
}
</style>
