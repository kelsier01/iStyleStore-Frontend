<script setup>
import FormPreguntas from './FormPreguntas.vue'
import { ref } from 'vue'

// Creamos una variable reactiva para almacenar el estado seleccionado
const estadoSeleccionado = ref('1'); // Por defecto, seleccionamos la opción 'Prendido'

// Función que se ejecuta cuando cambia la opción seleccionada
const handleChange = () => {
  // Aquí puedes realizar cualquier lógica adicional que necesites
  console.log('Estado seleccionado:', estadoSeleccionado.value);
}
</script>

<template>
  <form class="col-12">
    <div class="">
      <div class="card-body row">
        <div class="col-10">
          <div class="row">
            <div class="col-3">
              1.-En que estado ingresa el celular
            </div>
            <div class="col-3">
              <select class="form-control" v-model="estadoSeleccionado" @change="handleChange">
                <option value="1">Prendido</option>
                <option value="2">Apagado</option>
                <option value="3">Bloqueado</option>
              </select>
            </div>
          </div>
        </div>
        <div class="col-2"></div>
        <div class="col-12">
          <!-- Utilizamos v-if para condicionalmente renderizar el componente FormPreguntas -->
          <FormPreguntas v-if="estadoSeleccionado === '1'"/>
          <br/>
          <label>Observacion</label> 
          <textarea name="textarea" rows="4" class="form-control mt-2 mb-5 large-textarea"></textarea>
        </div>
        <div class="col-12 text-right">
          <button class="btn btn-primary botonguardar waves-effect waves-light">Guardar</button>
        </div>
      </div> 
    </div>         
  </form>
</template>

<style>
    
</style>
