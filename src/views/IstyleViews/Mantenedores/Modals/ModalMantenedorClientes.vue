<script setup>
import axios from "axios";
import { reactive, watch } from "vue";
import Swal from "sweetalert2";

const props = defineProps(["dataCliente", "estado"]);
const emit = defineEmits(["updateCliente", "agregarCliente"]);

const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const editarCliente = reactive({
  nombre: null,
  run: null,
  mail: null,
  fono: null,
  estado: 1,
});
watch(
  () => props.dataCliente,
  (Cliente, prevCliente) => {
    if (Cliente !== prevCliente) {
      editarCliente.nombre = props.dataCliente.nombre;
      editarCliente.run = props.dataCliente.run;
      editarCliente.mail = props.dataCliente.mail;
      editarCliente.fono = props.dataCliente.fono;
      editarCliente.estado = props.dataCliente.estado;
    }
  }
);

function actualizarCliente() {
  axios
    .put(rutaAPI + "clientes/" + props.dataCliente.id, editarCliente, token)
    .then((response) => {
      if (response.data) {
        emit("updateCliente", response.data);
        Swal.fire({
          title: "Excelente!",
          text: "Datos almacenado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
        });
      }
    });
}
function nuevoCliente(){
  axios.post(rutaAPI + "clientes/", editarCliente, token)
  .then((response) => {
    if(response.data){
      emit("agregarCliente");
      Swal.fire({
          title: "Excelente!",
          text: "Datos almacenado correctamente!",
          icon: "success",
          confirmButtonText: "OK",
      });
    }
  }).catch((error)=>{
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
        <BaseBlock title="Editar Cliente" transparent class="mb-0">
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
                <label for="modal-block-small-nombre">Nombre Cliente: </label>
                <input
                  type="text"
                  class="form-control mb-3"
                  id="modal-block-small-nombre"
                  :value="props.estado === 0 ? editarCliente.nombre : ''"
                  @input="editarCliente.nombre = $event.target.value"
                />

                <label for="modal-block-small-run">Run Cliente:</label>
                <input
                  type="text"
                  class="form-control mb-3"
                  :value="props.estado === 0 ? editarCliente.run : ''"
                  id="modal-block-small-run"
                  @input="editarCliente.run = $event.target.value"
                />

                <label for="modal-block-small-mail">Email Cliente:</label>
                <input
                  type="text"
                  class="form-control mb-3"
                  :value="props.estado === 0 ? editarCliente.mail : ''"
                  id="modal-block-small-mail"
                  @input="editarCliente.mail = $event.target.value"
                />

                <label for="modal-block-small-fono">Contacto Cliente:</label>
                <input
                  type="text"
                  class="form-control mb-3"
                  :value="props.estado === 0 ? editarCliente.fono : ''"
                  id="modal-block-small-fono"
                  @input="editarCliente.fono = $event.target.value"
                />

                <label for="modal-block-small-estado" class="modal-block-small-name">Estado:</label>
                <select 
                    name="modal-block-small-estado" 
                    id="modal-block-small-estado"
                    class="form-control mb-3 mt-3"
                    v-model="editarCliente.estado"
                    v-if="props.estado === 0"
                >
                  <option value="0">Deshabilitado</option>
                  <option value="1">Habilitado</option>
                </select>
                <select 
                    name="modal-block-small-estado" 
                    id="modal-block-small-estado"
                    class="form-control mb-3 mt-3"
                    @change="editarCliente.estado = $event.target.value"
                    :value=1
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
                @click="actualizarCliente"
                v-if="props.estado == 0"
              >
                Actualizar
              </button>
              <button
                type="button"
                class="btn btn-sm btn-dark"
                data-bs-dismiss="modal"
                @click="nuevoCliente"
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
