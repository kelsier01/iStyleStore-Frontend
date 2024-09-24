<script setup>
import axios from "axios";
import { reactive, watch } from "vue";
import Swal from "sweetalert2";

const props = defineProps(["dataServicio", "estado"]);
const emit = defineEmits(["updateServicio", "agregarServicio"]);

const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const editarServicio = reactive({
  nombre: null,
  precio: null,
  estado: 1,
});
watch(
  () => props.dataServicio,
  (Servicio, prevServicio) => {
    if (Servicio !== prevServicio) {
      editarServicio.nombre = props.dataServicio.nombre;
      editarServicio.precio = props.dataServicio.precio;
      editarServicio.estado = props.dataServicio.estado;
    }
  }
);
function actualizarServicio() {
  axios
    .put(rutaAPI + "servicios/" + props.dataServicio.id, editarServicio, token)
    .then((response) => {
      if (response.data) {
        emit("updateServicio", response.data);
        Swal.fire({
          title: "Excelente!",
          text: "Datos actualizado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
        });
      }
    });
}

function nuevoServicio() {
  axios
    .post(rutaAPI + "servicios/", editarServicio, token)
    .then((response) => {
      if (response.data) {
        emit("agregarServicio");
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
        <BaseBlock title="Agregar Bodegas" transparent class="mb-0">
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
                <label for="modal-block-small-name">Nombre Servicio:</label>
                <input
                  type="text"
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-name"
                  name="modal-block-small-name"
                  :value="props.estado === 0 ? editarServicio.nombre : ''"
                  @input="editarServicio.nombre = $event.target.value"
                />
              </div>
              <div class="form-group">
                <label for="modal-block-small-precio">Precio: </label>
                <input
                  type="text"
                  class="form-control mb-3 mt-3"
                  id="modal-block-small-precio"
                  name="modal-block-small-precio"
                  :value="props.estado === 0 ? editarServicio.precio : ''"
                  @input="editarServicio.precio = $event.target.value"
                />
              </div>
              <div class="form-group">
                <label for="modal-block-small-precio">Estado: </label>
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  v-model="editarServicio.estado"
                  v-if="props.estado === 0"
                >
                  <option value="0">Deshabilitado</option>
                  <option value="1">Habilitado</option>
                </select>
                <select
                  name="modal-block-small-estado"
                  id="modal-block-small-estado"
                  class="form-control mb-3 mt-3"
                  @change="editarServicio.estado = $event.target.value"
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
                @click="actualizarServicio"
                v-if="props.estado == 0"
              >
                Actualizar
              </button>
              <button
                type="button"
                class="btn btn-sm btn-dark"
                data-bs-dismiss="modal"
                @click="nuevoServicio"
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
