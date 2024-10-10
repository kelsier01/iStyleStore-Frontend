<script setup>
    import axios from 'axios';
    import { ref } from 'vue';
    const rutaAPI = import.meta.env.VITE_URL_API;
    const token = {
        headers: {
            "x-token": localStorage.getItem("Token"),
        },
    };
    const emit = defineEmits(['getData']);
    const nuevaPregunta = ref('');
    const registrarPregunta = () =>{
      if(nuevaPregunta.value.length > 0){
        axios.post(rutaAPI + "preguntas", {descripcion: nuevaPregunta.value, estado: 0}, token)
            .then((response) => {
                console.log(response);
                emit('getData');
            })
            .catch((error) => {
                console.log(error);
            });
      }
    };

</script>

<template>
    <button
        type="button"
        class="btn btn-dark col-1 offset-11 waves-effect waves-light"
        data-bs-toggle="modal"
        data-bs-target="#modal-block-small"
        >
        Agregar
    </button>
    
    <!-- Small Block Modal -->
    <div
      class="modal"
      id="modal-block-small"
      tabindex="-1"
      role="dialog"
      aria-labelledby="modal-block-small"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm" role="document">
        <div class="modal-content">
          <BaseBlock title="Agregar Preguntas" transparent class="mb-0">
            <template #options>
              <button
                type="button"
                class="btn-block-option"
                data-bs-dismiss="modal"
                aria-label="Close"
              >
                <i class="fa fa-fw fa-times"></i>
              </button>
            </template>

            <template #content>
              <div class="block-content fs-sm">
                <div class="form-group">
                  <label for="modal-block-small-name">Ingresar pregunta:</label>
                  <input
                    type="text"
                    class="form-control mb-3 mt-3"
                    id="modal-block-small-name"
                    name="modal-block-small-name"
                    v-model="nuevaPregunta"
                  />
                </div>
              </div>
              <div class="block-content block-content-full text-end bg-body">
                <button
                  type="button"
                  class="btn btn-sm btn-alt-secondary me-1"
                  data-bs-dismiss="modal"
                >
                  Cerrar
                </button>
                <button
                  type="button"
                  class="btn btn-sm btn-dark"
                  data-bs-dismiss="modal"
                  @click="registrarPregunta"
                >
                  Guardar
                </button>
              </div>
            </template>
          </BaseBlock>
        </div>
      </div>
    </div>
    <!-- END Small Block Modal -->
</template>

<style>
    
</style>