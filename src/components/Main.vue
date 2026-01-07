<template>
  <main class="flex-1 py-8 bg-[#f8f9fa]">
    <div class="max-w-[1200px] mx-auto px-8">
      <section class="text-center mb-12">
        <h2 class="text-[2.5rem] text-[#2c3e50] mb-4">Tu Próximo Partido Comienza Acá</h2>
        <p class="text-[1.2rem] text-[#666]">Descubrí las mejores canchas de Río Gallegos y viví la pasión del fútbol al máximo.</p>
      </section>

      <section class="canchas-list">
        <h3 class="text-[2rem] text-[#2c3e50] mb-8 text-center">Canchas Disponibles</h3>
        <div class="grid grid-cols-[repeat(auto-fit,minmax(280px,1fr))] gap-4 px-2">
          <div v-for="cancha in canchas" :key="cancha.id" class="bg-white rounded-xl overflow-hidden shadow-[0_4px_15px_rgba(0,0,0,0.1)] transition-transform duration-300 hover:-translate-y-[5px]">
            <img :src="cancha.imagen" :alt="cancha.nombre" class="w-full h-[160px] object-cover">
            <div class="p-4">
              <h4 class="text-[1.1rem] text-[#2c3e50] mb-[0.3rem]">{{ cancha.nombre }}</h4>
              <p class="text-[#666] my-[0.2rem] text-[0.9rem]">{{ cancha.ubicacion }}</p>
              <p class="text-[#666] my-[0.2rem] text-[0.9rem]">{{ cancha.tipo }}</p>
              <p class="text-[1rem] font-bold text-[#27ae60] my-[0.3rem]">{{ cancha.telefono }}</p>
              <div class="flex flex-wrap gap-[0.4rem] my-[0.5rem]">
                <span v-for="caracteristica in cancha.caracteristicas" :key="caracteristica" class="bg-[#e3f2fd] text-[#1976d2] px-[0.6rem] py-[0.2rem] rounded-[20px] text-[0.75rem]">
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
import laCurtiembreImg from '../assets/Curtiembre.png'
const canchas = ref([
  {
    id: 1,
    nombre: 'La Gambeta Rg',
    ubicacion: 'Pres. Dr. Raúl R. Alfonsín 237',
    tipo: 'Fútbol 5, Futbol 6',
    telefono: '2966 58-8195' ,
    imagen: laGambetaImg,
    caracteristicas: ['Césped sintético','Techo', 'Iluminación', 'Vestuarios']
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
    telefono: '2966 70-1870',
    imagen: diasImg,
    caracteristicas: ['Césped sintético','Techo', 'Estacionamiento']
  },
  {
    id: 5,
    nombre: 'Hispano',
    ubicacion: 'Bartolomé Mitre 400-498',
    tipo: 'Fútbol 11, Fútbol 8',
    telefono: '2966 46-7395',
    imagen: hispanoImg,
    caracteristicas: ['Césped sintético','Iluminación', 'Estacionamiento']
  },
  {
    id: 6,
    nombre: 'Polideportivo Yatel  ',
    ubicacion: 'Av. Parque Industrial 645',
    tipo: 'Fútbol 5, Fútbol 6',
    telefono: '2966 52-5761',
    imagen: yatelImg,
    caracteristicas: ['Césped sintético', 'Iluminación', 'Estacionamiento', 'Cancha adentro']
  }
  ,{
    id: 7,
    nombre: 'La Curtiembre',
    ubicacion: 'Facundo Quiroga 99-199',
    tipo: 'Fútbol 5, Fútbol 6',
    telefono: '2966 41-2650',
    imagen: laCurtiembreImg,
    caracteristicas: ['Césped sintético', 'Iluminación', 'Estacionamiento', 'Cancha adentro']
  }
])
</script>
