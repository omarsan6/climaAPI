<script setup>

    import {reactive, ref} from 'vue'
    import Alerta from '../components/Alerta.vue'

    const busqueda = reactive({
        ciudad: '',
        pais: '-- Seleccione un pais --'
    })

    const error = ref('')

    const emits = defineEmits(['obtener-clima'])

    const paises = [
        { codigo: 'US', nombre: 'Estados Unidos' },
        { codigo: 'MX', nombre: 'México' },
        { codigo: 'AR', nombre: 'Argentina' },
        { codigo: 'CO', nombre: 'Colombia' },
        { codigo: 'CR', nombre: 'Costa Rica' },
        { codigo: 'ES', nombre: 'España' },
        { codigo: 'PE', nombre: 'Perú' }
    ]

    const consultarClima = () => {
        if(Object.values(busqueda).includes('')){
            error.value = 'Todos los campos son obligatorios'
            return
        }

        error.value = ''

        emits('obtener-clima', busqueda)
    }

</script>

<template>
    
    <form 
        class="formulario"
        @submit.prevent="consultarClima">

        <Alerta v-if="error" >{{ error }}</Alerta>

        <div class="campo">
            <label for="">Ciudad</label>
            <input 
                v-model="busqueda.ciudad"
                type="text"  
                id="ciudad"
                placeholder="Ingresa la ciudad">
        </div>
        
        <div class="campo">
            <label for="pais">Pais</label>
            <select 
                v-model="busqueda.pais"
                id="pais"
                >

                <option>
                    -- Seleccione un pais --
                </option>
                <option v-for="pais in paises" :value="pais.codigo">
                    {{ pais.nombre }}
                </option>
            </select>
        </div>

        <input type="submit" value="Consultar">
    </form>


</template>


