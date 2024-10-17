<script setup>
import axios from "axios";
import { ref, watch } from "vue";

const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
//Props
const props = defineProps([
  "estado",
  "pregunta",
  "pregunta_id",
]);
//Se actualiza la tabla con los datos nuevos
const emit = defineEmits(["getData"]);
const nuevaPregunta = ref(props.pregunta);

//Crear pregunta
const registrarPregunta = () => {
  if (nuevaPregunta.value.length > 0) {
    axios
      .post(rutaAPI + "preguntas", { descripcion: nuevaPregunta.value }, token)
      .then((response) => {
        if(response){
          emit("getData");
        }
      })
      .catch((error) => {
        console.log(error)
      });
  }
};

//Editar pregunta
const editarPregunta = () => {
  console.log(props.pregunta_id);
  axios
    .put(
      rutaAPI + "preguntas/" + props.pregunta_id,
      {
        descripcion: nuevaPregunta.value,
      },
      token
    )
    .then((response) => {
      if(response){
       emit("getData"); 
      }
    })
    .catch((error) => {
      console.log(error);
    });
};

watch(
  () => props.pregunta,
  (newPregunta) => {
    nuevaPregunta.value = newPregunta;
  }
);
</script>

<template>
  <div
    class="modal"
    id="modal-block-small"
    tabindex="-1"
    role="dialog"
    aria-labelledby="modal-block-small"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered modal-md" role="document">
      <div class="modal-content">
        <BaseBlock
          :title="props.estado == 0 ? 'Crear' : 'Editar'"
          transparent
          class="mb-0"
        >
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
                @click="
                  props.estado === 1 ? editarPregunta() : registrarPregunta()
                "
              >
                {{ props.estado === 1 ? "Editar" : "Guardar" }}
              </button>
            </div>
          </template>
        </BaseBlock>
      </div>
    </div>
  </div>
  <!-- END Small Block Modal -->
</template>

<style></style>
