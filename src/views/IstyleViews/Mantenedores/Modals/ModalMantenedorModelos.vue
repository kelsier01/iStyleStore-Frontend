<script setup>
import Swal from "sweetalert2";
import axios from "axios";
import { reactive, watch } from "vue";
import { ref } from "vue";
import { computed } from "vue";

const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const props = defineProps(["dataModelo", "dataEquipo", "estado"]);
const emit = defineEmits(["updateModelo", "guardarModelo"]);
const editarModelo = reactive({
  nombre: null,
  estado: 1,
  modelo: null,
  nombreEquipo: null,
});
watch(
  () => props.dataModelo,
  (Modelo, prevModelo) => {
    if (Modelo !== prevModelo) {
      editarModelo.nombre = props.dataModelo.nombre;
      editarModelo.estado = props.dataModelo.estado;
      editarModelo.modelo = props.dataModelo.modelo;
    }
  }
);

function actualizarModelo() {
  axios
    .put(rutaAPI + "modelos/" + props.dataModelo.id, editarModelo, token)
    .then((response) => {
      if (response.data) {
        response.data.nombreEquipo = equipoSeleccionado.value;
        console.log(response.data);
        emit("updateModelo", response.data);
        Swal.fire({
          title: "Excelente!",
          text: "Datos actualizado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
        });
      }
    });
}
function nuevoModelo() {
  axios.post(rutaAPI + "modelos/", editarModelo, token).then((response) => {
    if (response) {
      emit("guardarModelo");
      Swal.fire({
        title: "Excelente!",
        text: "Datos actualizado correctamente!",
        icon: "success",
        confirmButtonText: "OK",
      });
    }
  });
}

const equipoSeleccionado = computed(() => {
  const equipo = props.dataEquipo.find(
    (equipo) => equipo.id === editarModelo.modelo
  );
  return equipo ? equipo.nombre : "";
});
</script>

<template>
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
        <BaseBlock title="Editar Modelo" transparent class="mb-0">
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
                <label for="modal-block-small-name">Nombre Equipos:</label>
                <input
                  type="text"
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-name"
                  name="modal-block-small-name"
                  :value="props.estado === 0 ? editarModelo.nombre : ''"
                  @input="editarModelo.nombre = $event.target.value"
                />
              </div>
              <div class="form-group">
                <label for="modal-block-small-equipo">Elige un modelo: </label>
                <select
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-equipo"
                  name="modal-block-small-equipo"
                  v-model="editarModelo.modelo"
                  v-if="props.estado === 0"
                >
                  <option v-for="equipo in props.dataEquipo" :value="equipo.id">
                    {{ equipo.nombre }}
                  </option>
                </select>
                <select
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-equipo"
                  name="modal-block-small-equipo"
                  v-else-if="props.estado === 1"
                  @change="editarModelo.modelo = $event.target.value"
                  :value="1"
                >
                  <option v-for="equipo in props.dataEquipo" :value="equipo.id">
                    {{ equipo.nombre }}
                  </option>
                </select>
              </div>
              <div class="form-group">
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  v-model="editarModelo.estado"
                  v-if="props.estado === 0"
                >
                  <option value="0">Deshabilitado</option>
                  <option value="1">Habilitado</option>
                </select>
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  @change="editarModelo.estado = $event.target.value"
                  :value="1"
                  v-else-if="props.estado === 1"
                >
                  <option value="0">Deshabilitado</option>
                  <option value="1">Habilitado</option>
                </select>
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
                @click="actualizarModelo"
                v-if="props.estado == 0"
              >
                Actualizar
              </button>
              <button
                type="button"
                class="btn btn-sm btn-dark"
                data-bs-dismiss="modal"
                @click="nuevoModelo"
                v-else-if="props.estado == 1"
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

<style></style>
