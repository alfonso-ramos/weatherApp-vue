<script setup>
import { reactive, ref } from 'vue';
import Alerta from './Alerta.vue';

const busqueda = reactive({
    ciudad: "",
    pais: ""
})

const error = ref("")


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
        error.value = "Todos los campos son obligatorios"
        return
    }
    error.value = ''
}

</script>
<template>
    <form 
        @submit.prevent="consultarClima"
        class="formulario"
    >
        <Alerta v-if="error" >{{ error }}</Alerta>
        <div class="campo">
            <label for="ciudad"></label>
            <input v-model="busqueda.ciudad" id="ciudad" type="text" placeholder="Ciudad">
        </div>
        <div class="campo">
            <label for="pais"></label>
            <select 
                v-model="busqueda.pais" 
                name="pais" id="pais"
            >
                <option value="">--- SELECCIONE UN PAIS ---</option>
                <option v-for="pais in paises" :value="pais.codigo">
                    {{ pais.nombre }}
                </option>

            </select>
        </div>
        <input type="submit" value="Consultar clima">
    </form>
</template>
