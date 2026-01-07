<template>
  <main class="main">
    <div class="container">
      <section class="hero">
        <h2>Tu Próximo Partido Comienza Acá</h2>
        <p>Descubrí las mejores canchas de Río Gallegos y viví la pasión del fútbol al máximo.</p>
      </section>

      <section class="canchas-list">
        <h3>Canchas Disponibles</h3>
        <div class="canchas-grid">
          <div v-for="cancha in canchas" :key="cancha.id" class="cancha-card">
            <img :src="cancha.imagen" :alt="cancha.nombre" class="cancha-imagen">
            <div class="cancha-info">
              <h4>{{ cancha.nombre }}</h4>
              <p class="ubicacion">{{ cancha.ubicacion }}</p>
              <p class="tipo">{{ cancha.tipo }}</p>
              <p class="telefono">{{ cancha.telefono }}</p>
              <div class="caracteristicas">
                <span v-for="caracteristica in cancha.caracteristicas" :key="caracteristica" class="tag">
                  {{ caracteristica }}
                </span>
              </div>
              </div>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue'

// Importar imágen
import laGambetaImg from '../assets/La Gambeta.png'
import talleresImg from '../assets/Talleres.png'
import fairplayImg from '../assets/Fairplay.png'
import diasImg from '../assets/Dias.png'
import hispanoImg from '../assets/Hispano.png'
import yatelImg from '../assets/Yatel.png'

const canchas = ref([
  {
    id: 1,
    nombre: 'La Gambeta Rg',
    ubicacion: 'Pres. Dr. Raúl R. Alfonsín 237',
    tipo: 'Fútbol 5, Futbol 6',
    telefono: '2966 58-8195' ,
    imagen: laGambetaImg,
    caracteristicas: ['Techo', 'Iluminación', 'Vestuarios']
  },
  {
    id: 2,
    nombre: 'Talleres',
    ubicacion: 'Mariano Moreno 157',
    tipo: 'Fútbol 7, Fútbol 6',
    telefono: '2966 44-7975',
    imagen: talleresImg,
    caracteristicas: ['Césped sintético', 'Iluminación', 'Estacionamiento',  'Cancha adentro']
  },
  {
    id: 3,
    nombre: 'Fairplay',
    ubicacion: 'Av. Parque Industrial 801-899',
    tipo: 'Fútbol 5, Fútbol 6',
    telefono: '',
    imagen: fairplayImg,  
    caracteristicas: ['Techo', 'Iluminación', 'Estacionamiento']
  },
  {
    id: 4,
    nombre: 'Polideportivo Diaz',
    ubicacion: 'Juan Bark y Río Grande',
    tipo: 'Fútbol 5',
    telefono: '02966 70-1870',
    imagen: diasImg,
    caracteristicas: ['Techo', 'Estacionamiento']
  },
  {
    id: 5,
    nombre: 'Hispano',
    ubicacion: 'Bartolomé Mitre 400-498',
    tipo: 'Fútbol 11, Fútbol 8',
    telefono: '2966 46-7395',
    imagen: hispanoImg,
    caracteristicas: ['Iluminación', 'Estacionamiento']
  },
  {
    id: 6,
    nombre: 'Polideportivo Yatel  ',
    ubicacion: 'Av. Parque Industrial 645',
    tipo: 'Fútbol 5, Fútbol 6',
    telefono: '02966 70-1870',
    imagen: yatelImg,
    caracteristicas: ['Techo', 'Iluminación', 'Estacionamiento', 'Cancha adentro']
  }
])
</script>

<style scoped>
.main {
  flex: 1;
  padding: 2rem 0;
  background: #f8f9fa;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.hero {
  text-align: center;
  margin-bottom: 3rem;
}

.hero h2 {
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 1rem;
}

.hero p {
  font-size: 1.2rem;
  color: #666;
}

.canchas-list h3 {
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 2rem;
  text-align: center;
}


.canchas-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1rem;
  padding: 0 0.5rem;
}

.cancha-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s;
}

.cancha-card:hover {
  transform: translateY(-5px);
}

.cancha-imagen {
  width: 100%;
  height: 160px;
  object-fit: cover;
}

.cancha-info {
  padding: 1rem;
}

.cancha-info h4 {
  font-size: 1.1rem;
  color: #2c3e50;
  margin-bottom: 0.3rem;
}

.ubicacion, .tipo {
  color: #666;
  margin: 0.2rem 0;
  font-size: 0.9rem;
}

.telefono {
  font-size: 1rem;
  font-weight: bold;
  color: #27ae60;
  margin: 0.3rem 0;
}

.caracteristicas {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin: 0.5rem 0;
}

.tag {
  background: #e3f2fd;
  color: #1976d2;
  padding: 0.2rem 0.6rem;
  border-radius: 20px;
  font-size: 0.75rem;
}



</style>