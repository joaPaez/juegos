<script setup>
import { ref, computed } from 'vue';

let juegoN = ref({
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
    nombre: juegoN.value.nombre,
    plataforma: juegoN.value.plataforma,
    estado: juegoN.value.estado,
    puntuacion: juegoN.value.puntuacion,
  });

  // Limpiar el formulario después de agregar el juego
  juegoN.value.nombre = '';
  juegoN.value.plataforma = 'elegir';
  juegoN.value.estado = 'elegir';
  juegoN.value.puntuacion = '';
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
    <input type="text" id="nombre" placeholder="Nombre del juego" v-model="juegoN.nombre">
    <br>
    <label for="">Plataforma</label>
    <select name="Plataforma" id="plataforma" v-model="juegoN.plataforma">
      <option value="elegir">Elige una plataforma</option>
      <option value="PC">PC</option>
      <option value="PlayStation">PlayStation</option>
      <option value="Xbox One">Xbox One</option>
    </select>
    <br>
    <label for="">Estado</label>
    <select name="Estado" id="estado" v-model="juegoN.estado">
      <option value="elegir">Elige un estado</option>
      <option value="Pendiente">Pendiente</option>
      <option value="Jugando">Jugando</option>
      <option value="Completado">Completado</option>
    </select>
    <br>
    <label for="">Puntuación</label>
    <input type="text" id="puntuacion" placeholder="Valor numérico del 1 al 10" v-model="juegoN.puntuacion">
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
      <td>{{ i.plataforma }}</td>
      <td>{{ i.estado }}</td>
      <td>{{ i.puntuacion }}</td>
    </tr>
  </table>
</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  padding: 20px;
}

h1 {
  text-align: center;
  font-size: 24px;
  margin-bottom: 20px;
}

form {
  background-color: #e8e8e8;
  padding: 20px;
  border-radius: 5px;
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"],
select {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

button {
  display: inline-block;
  padding: 10px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

table, th, td {
  border: 1px solid #ccc;
}

th, td {
  padding: 12px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

div {
  padding: 10px;
  background-color: #f4f4f4;
  border-radius: 5px;
}
</style>