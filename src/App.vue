<script setup>

import { ref, reactive, onMounted  } from 'vue'
import {db} from './data/guitarrasbd' //Estoy importando la base de datos y la llame db

// Conponente 
//-No se coloca los componentes 
import Header from './components/Header.vue'
import  Guitarra  from "./components/Guitarra.vue";
import  Footer  from "./components/footer.vue";

// Ejemplo con reactive
// const state = reactive({  
//  guitarras : [db] //Arrary de guitarras que lo volvemos reactive 
// })


//Ejemplo con Ref
const guitarras = ref([]) 

//para agregar todo al carrito y almacenarlo 
const carrito = ref([]) 

onMounted( () =>{  //Conponente este listo va ejecutarce
 guitarras.value = db  //(ref) 
 //state.guitarras = bd  //para (reactive) este se uliza en un opjeto relaccionado
})

//parsar a un componente la funcion para hacer el evento
 //(guitarra) - le estoy mandando un opjeto desde el evento que esta en el archivo Guitarra 
 const agregarCarrito = (guitarra) => {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra); //estoy agregando la guitarra al array de carrito
  } 

</script>

<template>
   <!-- Componente header-->
   <!-- (:carrito="carrito") le estoy mandondo el array donde tiene toda la informacion del carrito-->
   <Header :carrito="carrito"></Header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
           <!-- Renderizar para que muestre el componente -->
           <!-- (:guitarra="guitarra") estoy mandando   -->
           <Guitarra v-for="guitarra in guitarras" 
                     :guitarra="guitarra" 
                     @agregar-Carrito="agregarCarrito">
           </Guitarra> 
        </div>
    </main>

    <!-- Componente footer-->
    <Footer></Footer>
    
</template>
