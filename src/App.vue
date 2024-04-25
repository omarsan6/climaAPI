<script setup>
  import Formulario from './components/Formulario.vue'
  import Clima from './components/Clima.vue'
  import Spiner from './components/Spiner.vue'
  import Alerta from './components/Alerta.vue'
  import useClima from './composables/useClima.js'

  const {obtenerClima, clima,mostrarClima,cargando,error} = useClima()



</script>

<template>

  <h1 class="titulo">Buscador de clima</h1>

  <div class="contenedor buscador-clima">
    <Formulario
      @obtener-clima="obtenerClima"/>

    <Alerta v-if="error">{{ error }}</Alerta>
    
    <Spiner v-if="cargando"/>

    <Clima 
      v-if="mostrarClima" 
      :clima="clima"/>
  </div>

</template>

<style scoped>

</style>
