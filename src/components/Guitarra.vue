<!--Componente-->
<script setup>
// import { ref } from 'vue';
// const numero = ref(0) //inicializa en 0 

  const props = defineProps({  //para definir y tomar la infomacion que estoy mandando en los props
    guitarra:{   //definiendo el objeto
        type: Object,
        require: true
    }
  })

// //Funcion de incremento para hacer el evento del click
//   const incrementar = () => {
//     numero.value++
//   } 

//Declarar el evento que llega de App
defineEmits('agregar-Carrito')

</script>

<template>
          <div class="col-md-6 col-lg-4 my-4 row align-items-center">
                <div class="col-4">
                    <!--Se puede colocar  v-bing:src o :scr para mostrar una imagen reactiva -->
                    <img class="img-fluid" :src="'/img/'+ guitarra.imagen + '.jpg'" alt="imagen guitarra">
                </div>
                <div class="col-8">
                    <h3 class="text-black fs-4 fw-bold text-uppercase">{{guitarra.nombre}}</h3>
                    <!-- <p>{{numero}}</p> Nota: Aqui no es necesario de colocar numero.value por que esta en el template -->
                    <p>{{guitarra.descripcion}}</p>
                    <p class="fw-black text-primary fs-3">{{guitarra.precio}}</p>
                    <button 
                        type="button"
                        class="btn btn-dark w-100 "   
                        @click="$emit('agregar-Carrito', guitarra)" 
                    >Agregar al Carrito</button>
                    <!-- Eventos de click -->
                    <!-- Forma larga v-on:click="incrementar" -->
                    <!-- Forma corta @click="incrementar" -->
                    <!-- @click="$emits=('agregar-Carrito', guitarra)" //le mando el objeto a la funcion de agregacarrito (archivo = App)-->
                </div>
            </div><!-- FIN GUITARRA -->
</template>


<style lang="scss" scoped>

</style>