<template>
  <!-- Dentro del template las const no necesitan .value -->
  <h2>Cena {{ contador + 1 }} con el rey {{ rey }}</h2>

  <h3 class="precio">Precio: ${{ productos[contador].precio }} Ars</h3>

  <div class="fs dias" v-if="productos[contador].finDeSemana === true">(Solo fines de Semana)</div>

  <div class="td dias" v-else>(De Lunes a Domingo)</div>

  <div vx-if="productos[contador].precio < 100" class="oferta">
    <div>Ahora un 10% descuento: ${{ nuevoPrecio }}Ars</div>
    <img src="/oferta.jpg" alt="oferta" />
  </div>

  <img :src="imagen" alt="imagen" />

  <button @:click="siguiente">Siguiente ({{ contador + 1 }} / {{ total }} )</button>
</template>

<script setup>
import { computed, ref } from "vue";
import { productos } from "./datos.js";
const contador = ref(0);
const total = productos.length;
const ruta = "https://www.html6.es/img/rey_";
const siguiente = () => {
  contador.value++;
  if (contador.value >= total) {
    contador.value = 0;
  }
};
const rey = computed(() => {
  const elNombre = productos[contador.value].nombre.toLowerCase();
  //como estoy fuera del template debo agregar .value

  return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1);
});
const imagen = computed(() => {
  return `${ruta}${productos[contador.value].nombre.toLocaleLowerCase()}.png`;
});

const nuevoPrecio = computed(() => {
  return Number(productos[contador.value].precio / 1.1).toFixed(2);
});
</script>

<style scoped>
.td {
  background-color: green;
}
.fs {
  background-color: red;
}
.dias {
  color: white;
  padding: 4px 17px;
  font-size: 0.9em;
  border-radius: 4px;
  margin: 5px 0 10px;
  display: inline-block;
}
.oferta img {
  width: 65px;
  margin: 12px 5px;
}
</style>
