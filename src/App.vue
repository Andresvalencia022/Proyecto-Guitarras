<script setup>
import { ref, reactive, onMounted } from "vue";
import { db } from "./data/guitarrasbd"; //Estoy importando la base de datos y la llame db

// Conponente
//-No se coloca los componentes
import Header from "./components/Header.vue";
import Guitarra from "./components/Guitarra.vue";
import Footer from "./components/footer.vue";

// Ejemplo con reactive
// const state = reactive({
//  guitarras : [db] //Arrary de guitarras que lo volvemos reactive
// })

//Ejemplo con Ref
const guitarras = ref([])
const carrito = ref([])//para agregar todo al carrito y almacenarlo
const guitarra = ref({})//trabajar con un objeto 

onMounted(() => {
  //Conponente este listo va ejecutarce
  guitarras.value = db //(ref)
  guitarra.value = db[3] //estoy accediendo al objeto que esta en la posicion 3 

  //state.guitarras = bd  //para (reactive) este se uliza en un opjeto relaccionado
});

//parsar a un componente la funcion para hacer el evento
//(guitarra) - le estoy mandando un opjeto desde el evento que esta en el archivo Guitarra
const agregarCarrito = (guitarra) => {
  // comprovar si existe
  const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)

  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++ //[existeCarrito].cantidad++ indentifica y actualiza la cantidad en el array (lo incrementa)
  } else {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra); //estoy agregando la guitarra al array de carrito
  }
}

 //Funicion de decremento e incremento
  const disminuirCantidad = (id) => {
      const index = carrito.value.findIndex(producto => producto.id === id)
      if (carrito.value[index].cantidad <= 1 ) return //condición que valida si es menor o igual a 1 no  permita hacer la función de decrementar
      carrito.value[index].cantidad--
  }
  const incrementoCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if (carrito.value[index].cantidad >= 5 ) return //Condicion que valida 1 que si es mayor a 5 no  permita hacer la función de incrementar
    carrito.value[index].cantidad++ 
  }
</script>

<template>
  <!-- Componente header-->
  <!-- (:carrito="carrito") le estoy mandondo el array donde tiene toda la informacion del carrito-->
  <Header :carrito="carrito"
          :guitarra="guitarra"
           @disminuir-cantidad="disminuirCantidad"
           @incremento-cantidad="incrementoCantidad"
           @agregar-Carrito="agregarCarrito">

  </Header>

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <!-- Renderizar para que muestre el componente -->
      <!-- (:guitarra="guitarra") estoy mandando   -->
      <Guitarra
        v-for="guitarra in guitarras"
        :guitarra="guitarra"
        @agregar-Carrito="agregarCarrito"
      >
      </Guitarra>
    </div>
  </main>

  <!-- Componente footer-->
  <Footer></Footer>
</template>
