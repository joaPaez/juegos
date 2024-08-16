<script setup>
import { ref, computed } from 'vue';

let juego = ref({
  nombre: '',
  plataforma: 'elegir',
  estado: 'elegir',
  puntuacion: '',
});

let juegos = ref([]);

let busnombre = ref('');
let busplataforma = ref('');
let busestado = ref('');

// Agregar un nuevo juego a la lista
function agregarjuego() {
  juegos.value.push({
    nombre: juego.value.nombre,
    plataforma: juego.value.plataforma,
    estado: juego.value.estado,
    puntuacion: juego.value.puntuacion,
  });

  // Limpiar el formulario después de agregar el juego
  juego.value.nombre = '';
  juego.value.plataforma = 'elegir';
  juego.value.estado = 'elegir';
  juego.value.puntuacion = '';
}

// Computed property para obtener los juegos filtrados
const juegosFiltrados = computed(() => {
  return juegos.value.filter(juego => 
    juego.nombre.toLowerCase().includes(busnombre.value.toLowerCase()) &&
    juego.plataforma.toLowerCase().includes(busplataforma.value.toLowerCase())&&
    juego.estado.toLowerCase().includes(busestado.value.toLowerCase())
  );
});
</script>

<template>
  <h1>EJEMPLO PRACTICO</h1>
  <h1>Añadir juego</h1>
  <form action="">
    <label for="">Nombre</label>
    <input type="text" id="nombre" placeholder="Nombre del juego" v-model="juego.nombre">
    <br>
    <label for="">Plataforma</label>
    <select name="Plataforma" id="plataforma" v-model="juego.plataforma">
      <option value="elegir">Elige una plataforma</option>
      <option value="PC">PC</option>
      <option value="PlayStation">PlayStation</option>
      <option value="Xbox One">Xbox One</option>
    </select>
    <br>
    <label for="">Estado</label>
    <select name="Estado" id="estado" v-model="juego.estado">
      <option value="elegir">Elige un estado</option>
      <option value="Pendiente">Pendiente</option>
      <option value="Jugando">Jugando</option>
      <option value="Completado">Completado</option>
    </select>
    <br>
    <label for="">Puntuación</label>
    <input type="text" id="puntuacion" placeholder="Valor numérico del 1 al 10" v-model="juego.puntuacion">
    <br>
    <input type="button" @click="agregarjuego" value="Agregar Videojuego">
  </form>
  <br>
  <!-- Campo de búsqueda -->
   <h2>Buscar</h2>
   nombre
  <input type="text" v-model="busnombre" >
  plataforma
  <select name="" id="" v-model="busplataforma">
      <option value=""></option>  
      <option value="PC">PC</option>
      <option value="PlayStation">PlayStation</option>
      <option value="Xbox One">Xbox One</option>
  </select>
  estado
  <select name="Estado" id="estado" v-model="busestado">
      <option value=""></option>
      <option value="Pendiente">Pendiente</option>
      <option value="Jugando">Jugando</option>
      <option value="Completado">Completado</option>
    </select>
    <br>
    <h2>Documentación de juegos</h2>
  <table>
    <tr>
      <th>Nombre</th>
      <th>Plataforma</th>
      <th>Estado</th>
      <th>Puntuación</th>
    </tr>
    <!-- Mostrar los juegos filtrados -->
    <tr v-for="i in juegosFiltrados" :key="i.nombre">
      <td>{{ i.nombre }}</td>
      <td>{{ juego.plataforma }}</td>
      <td>{{ i.estado }}</td>
      <td>{{ i.puntuacion }}</td>
    </tr>
  </table>
</template>

<style scoped>
/* Estilos opcionales */
</style>
