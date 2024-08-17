<script setup>
import { ref, computed } from 'vue';

let juegoN = ref({
  nombre: '',
  plataforma: 'elegir',
  estado: 'elegir',
  puntuacion: '',
});

let juegos = ref([]);
let error= ref(false);
let error2= ref(false);
let busnombre = ref('');
let busplataforma = ref('');
let busestado = ref('');




// Agregar un nuevo juego a la lista
function verificar(){

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

if(juegoN.value.puntuacion>=1 &&
  juegoN.value.puntuacion<=10){
    error.value=false
  }
  else if(juegoN.value.puntuacion==""){
    error.value=false
  }
else{
  error.value=true
}

  if(juegoN.value.nombre == '' ||
    juegoN.value.plataforma=="elegir" ||
    juegoN.value.estado=="elegir"){
      error2.value=true
    }
  else{
    error2.value=false
  }


 //vericar si falta completar algun casillero o si la puntuacion tiene un numero del 1 al 10 o esta vacia
  if(juegoN.value.puntuacion>=1 && 
    juegoN.value.puntuacion<=10 && 
    juegoN.value.nombre !== '' && 
    juegoN.value.plataforma!=="elegir" &&
    juegoN.value.estado!=="elegir"
  ){
    error2.value=false
    error.value=false
    agregarjuego()
  }
  else if(juegoN.value.puntuacion==""&&
    juegoN.value.nombre !== '' && 
    juegoN.value.plataforma!=="elegir" &&
    juegoN.value.estado!=="elegir"

  ){
    error2.value=false
    error.value=false
    agregarjuego()
  }

}


// Computed property para obtener los juegos filtrados
const juegosFiltrados = computed(() => {
  return juegos.value.filter(juego => 
    juego.nombre.toLowerCase().includes(busnombre.value.toLowerCase()) &&
    juego.plataforma.toLowerCase().includes(busplataforma.value.toLowerCase()) &&
    juego.estado.toLowerCase().includes(busestado.value.toLowerCase())
  );
});




// Mostrar información del juego seleccionado
let juegoSeleccionado = ref(null);

function mostrarInfo(juego) {
  juegoSeleccionado.value = juego;
}

// Verifica si el juego es el seleccionado
function esSeleccionado(juego) {
  return juegoSeleccionado.value && juegoSeleccionado.value.nombre === juego.nombre;
}
</script>





<template>
  <h1>Administración de videojuegos</h1>
  <h2>Nuevo videojuego</h2>
  <form action="">
    <label for="">Nombre</label>
    <input type="text" id="nombre" placeholder="Cualquier texto" v-model="juegoN.nombre">
    <br>
    <label for="">Plataforma</label>
    <select name="Plataforma" id="plataforma" v-model="juegoN.plataforma">
      <option value="elegir">PC | PlayStation | Xbox One</option>
      <option value="PC">PC</option>
      <option value="PlayStation">PlayStation</option>
      <option value="Xbox One">Xbox One</option>
    </select>
    <br>
    <label for="">Estado</label>
    <select name="Estado" id="estado" v-model="juegoN.estado">
      <option value="elegir">Pendiente | Jugando | Completado</option>
      <option value="Pendiente">Pendiente</option>
      <option value="Jugando">Jugando</option>
      <option value="Completado">Completado</option>
    </select>
    <br>
    <label for="">Puntuación</label>
    <input type="text" id="puntuacion" placeholder="Valor numérico del 1 al 10" v-model="juegoN.puntuacion">
    <br>
    <input type="button" @click="verificar" value="Registrar videojuego">
    <p style="color: red" v-if="error">Se debe poner un numero entre el 1 al 10</p>
    <p style="color: red" v-if="error2">Faltan completar casilleros</p>
  </form>
  <br>

  <h2>Videojuegos</h2>
  <!-- Campo de búsqueda -->




  <div style="display: flex; gap: 10px;">
    <input type="text" v-model="busnombre" placeholder="Nombre">
    <select name="" id="" v-model="busplataforma">
        <option value="">Plataforma</option>
        <option value="PC">PC</option>
        <option value="PlayStation">PlayStation</option>
        <option value="Xbox One">Xbox One</option>
    </select>
    <select name="" id="" v-model="busestado">
        <option value="">Estado</option>
        <option value="Pendiente">Pendiente</option>
        <option value="Jugando">Jugando</option>
        <option value="Completado">Completado</option>
    </select>
  </div>
  




  <div style="display: flex;">
    <table>
      <tr>
        <th>Nombre</th>
        <th>Plataforma</th>
        <th>Estado</th>
        <th>Puntuación</th>
      </tr>
      <!-- Mostrar los juegos filtrados -->
      <tr 
        v-for="i in juegosFiltrados" 
        :key="i.nombre" 
        @click="mostrarInfo(i)" 
        :style="{backgroundColor: esSeleccionado(i) ? '#d3d3d3' : ''}"
        style="cursor: pointer;"
      >
        <td>{{ i.nombre }}</td>
        <td>{{ i.plataforma }}</td>
        <td>{{ i.estado }}</td>
        <td>{{ i.puntuacion }}</td>
      </tr>
    </table>





    <!-- Cuadro de información -->
    <div v-if="juegoSeleccionado" style="border: 1px solid black; margin-left: 20px; padding: 10px; width: 200px;">
      <p><strong>Nombre:</strong> {{ juegoSeleccionado.nombre }}</p>
      <p><strong>Plataforma:</strong> {{ juegoSeleccionado.plataforma }}</p>
      <p><strong>Estado:</strong> {{ juegoSeleccionado.estado }}</p>
      <p><strong>Puntuación:</strong> {{ juegoSeleccionado.puntuacion }}</p>
    </div>
  </div>
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

tr:hover {
  background-color: #e0e0e0;
}

div {
  padding: 10px;
  background-color: #f4f4f4;
  border-radius: 5px;
}
</style>