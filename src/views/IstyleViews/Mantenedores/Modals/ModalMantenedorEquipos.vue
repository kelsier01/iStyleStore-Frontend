<script setup>
import axios from "axios";
import { reactive, watch } from "vue";
import Swal from "sweetalert2";

const props = defineProps(["dataEquipo", "estado"]);
const emit = defineEmits(["updateEquipo", "agregarEquipo"]);

const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const editarEquipo = reactive({
  nombre: null,
  estado: 1,
});
watch(
  () => props.dataEquipo,
  (Equipo, prevEquipo) => {
    if (Equipo !== prevEquipo) {
      editarEquipo.nombre = props.dataEquipo.nombre;
      editarEquipo.estado = props.dataEquipo.estado;
    }
  }
);
function actualizarEquipo() {
  axios
    .put(rutaAPI + "equipos/" + props.dataEquipo.id, editarEquipo, token)
    .then((response) => {
      if (response.data) {
        emit("updateEquipo", response.data);
        Swal.fire({
          title: "Excelente!",
          text: "Datos actualizado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
        });
      }
    });
}
function nuevoEquipo() {
  axios
    .post(rutaAPI + "equipos/", editarEquipo, token)
    .then((response) => {
      if (response.data) {
        emit("agregarEquipo");
        Swal.fire({
          title: "Excelente!",
          text: "Datos almacenado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
        });
      }
    })
    .catch((error) => {
      console.log(error);
    });
}
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
        <BaseBlock title="Actualizar equipo" transparent class="mb-0">
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
                <label for="modal-block-small-name">Nombre Equipo:</label>
                <input
                  type="text"
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-name"
                  name="modal-block-small-name"
                  :value="props.estado === 0 ? editarEquipo.nombre : ''"
                  @input="editarEquipo.nombre = $event.target.value"
                />
              </div>
              <div class="form-group">
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  v-model="editarEquipo.estado"
                  v-if="props.estado === 0"
                >
                  <option value="0">Deshabilitado</option>
                  <option value="1">Habilitado</option>
                </select>
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  @change="editarEquipo.estado = $event.target.value"
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
                @click="actualizarEquipo"
                v-if="props.estado == 0"
              >
                Actualizar
              </button>
              <button
                type="button"
                class="btn btn-sm btn-dark"
                data-bs-dismiss="modal"
                @click="nuevoEquipo"
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
