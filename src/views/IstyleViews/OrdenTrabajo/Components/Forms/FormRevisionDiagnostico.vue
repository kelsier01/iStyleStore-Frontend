<!-- eslint-disable vue/no-mutating-props -->
<script setup>
import { onMounted, reactive, ref, watch } from "vue";
import axios from "axios";
import Swal from "sweetalert2";
import moment from "moment";

const props = defineProps(["getOrden", "updateEstado"]);
const emit = defineEmits(["setValores", "updateOrden"]);

const rutaAPI = "http://localhost:8000/api/";
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const allServicios = ref();
const obs = ref(null);
const checkNuevoServicio = ref(false);

const totales = reactive({
  total: 0,
});
const servicioNuevo = reactive({
  nombre: null,
  precio: null,
  created_at: moment().format("YYYY-MM-DDTHH:mm"),
});
const diagnostico = reactive({
  orden_id: null,
  responsable: localStorage.getItem("Nombre"),
  id_estado: 2,
  observacion: null,
  garantia_id: null,
  created_at: moment().format("YYYY-MM-DDTHH:mm"),
});
const listaServicios = reactive([]);

onMounted(() => {
  axios.get(rutaAPI + "servicios", token).then(function (response) {
    allServicios.value = response.data.servicios.map((item) => {
      item.tittle = item.nombre + " - $" + item.precio;
      return item;
    });
  });
});

watch(
  () => props.getOrden,
  (nuevo, anterior) => {
    if (nuevo !== anterior) {
      listaServicios.length = 0;
      diagnostico.orden_id = nuevo.id;
      obs.value = nuevo.observacion;
      diagnostico.id_estado = nuevo.estado;
      nuevo.ordenServicios.map((item) => {
        listaServicios.push(item);
      });
    }
  }
);

watch(
  () => props.updateEstado,
  (nuevo, anterior) => {
    if (nuevo !== anterior) {
      guardarDiagnostico(nuevo);
      console.log("entro al watch");
    }
  }
);

function guardarDiagnostico(nuevo_estado) {
  let alerta = 0;
  let success = false;

  if (diagnostico.observacion && diagnostico.id_estado > 0) {
    if (props.getOrden.estado == 4 && props.getOrden.id_ultima_garantia) {
      console.log("diagnostico garantia");
      diagnostico.garantia_id = props.getOrden.id_ultima_garantia;
    }
    axios.post(rutaAPI + "revisiones", diagnostico, token).then(() => {
      if (!success) {
        success = true;
      }
      diagnostico.id_estado = 0;
      diagnostico.observacion = null;
    });
  } else {
    alerta = alerta + 1;
  }
  if (listaServicios.length > props.getOrden.ordenServicios.length) {
    let data = [];
    listaServicios.map((item) => {
      if (item.nuevo == 1) {
        let params = {
          orden_id: props.getOrden.id,
          servicio_id: item.id,
          responsable: localStorage.getItem("Nombre"),
          garantia_id: item.garantia_id,
          created_at: moment().format("YYYY-MM-DDTHH:mm"),
        };
        data.push(params);
      }
    });
    axios.post(rutaAPI + "orden_servicios", data, token).then((response) => {
      if (!success) {
        success = true;
      }
      console.log(response.data);
    });
  } else {
    alerta = alerta + 1;
  }

  if (alerta == 2 && nuevo_estado < 5) {
    Swal.fire({
      title: "Sin efecto!",
      text: "No existen datos nuevos para almacenar!",
      icon: "info",
      confirmButtonText: "OK",
    });
  } else {
    // Actualizar ºOT
    emit("updateOrden", nuevo_estado);
    // Aqui
  }
}

function addServicioLista(value) {
  if (value) {
    value.nuevo = 1;
    value.garantia_id = null;
    if (props.getOrden.id_ultima_garantia) {
      value.garantia_id = props.getOrden.id_ultima_garantia;
    }
    let precio = value.precio;
    listaServicios.push(value);
    if (listaServicios.length == 1) {
      precio = value.precio - props.getOrden.soloRevision;
    }
    totales.total = totales.total + value.precio;
    emitValores(precio, 1);
  }
}

function deleteServicioLista(data) {
  const index = listaServicios.indexOf(data);

  if (index !== -1) {
    totales.total = totales.total - data.precio;
    listaServicios.splice(index, 1);
    emitValores(data.precio, 0);
  }
}

function emitValores(value, op) {
  emit("setValores", { value, op });
}

function agregarServicio() {
  if (servicioNuevo.nombre && servicioNuevo.precio) {
    axios.post(rutaAPI + "servicios", servicioNuevo, token).then((response) => {
      console.log(response.data);
      servicioNuevo.nombre = null;
      servicioNuevo.precio = null;
      addServicioLista(response.data);
      response.data.tittle =
        response.data.nombre + " - $" + response.data.precio;
      allServicios.value.push(response.data);
    });
  }
}
</script>

<template>
  <div class="card-body">
    <div class="row">
      <div class="col-12 col-md-6">
        <div class="row">
          <label>Observación:</label>
          <textarea
            disabled="disabled"
            name="falla"
            rows="4"
            v-model="obs"
            class="form-control mt-2 mb-5 large-textarea"
          ></textarea>
        </div>
        <div class="row" v-if="props.getOrden.estado < 5">
          <label>Diagnóstico o Reparación:</label>
          <textarea
            name="diagnostico"
            rows="4"
            v-model="diagnostico.observacion"
            class="form-control mt-2 mb-5 large-textarea"
          ></textarea>
        </div>
        <div class="row" v-if="props.getOrden.estado < 5">
          <div class="col-4">
            <label>Estados: </label>
          </div>
          <div class="col-8">
            <select class="form-control" v-model="diagnostico.id_estado">
              <option value="2">En diagnostico</option>
              <option value="3">Listo para Retirar</option>
              <option v-show="props.getOrden.estado == 4" value="4">
                Garantía
              </option>
            </select>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-6" v-if="props.getOrden.estado < 5">
        <div class="content">
          <div class="row">
            <div class="col-md-3"><label>Ingresar servicio:</label></div>
            <div class="col-md-6">
              <v-select
                @update:modelValue="addServicioLista"
                :options="allServicios"
                placeholder="Seleccione..."
                label="tittle"
              >
              </v-select>
            </div>
            <div class="col-md-3">
              <div class="form-chec pointer">
                <input
                  type="checkbox"
                  id="defaultCheck1"
                  class="form-check-input pointer"
                  v-model="checkNuevoServicio"
                />
                <label for="defaultCheck1" class="form-check-label pointer">
                  Crear Servicio
                </label>
              </div>
            </div>
          </div>
          <div class="row bg-light py-3" v-show="checkNuevoServicio">
            <div class="col-12 col-md-4">
              <label>Nombre servicio:</label>
              <input
                type="text"
                placeholder="Servicio"
                v-model="servicioNuevo.nombre"
                class="form-control form-control-sm"
              />
            </div>
            <div class="col-12 col-md-4">
              <label>Valor servicio:</label>
              <input
                type="number"
                placeholder="Valor"
                v-model="servicioNuevo.precio"
                class="form-control form-control-sm"
              />
            </div>
            <div class="col-12 col-md-4 text-center align-self-end">
              <button
                class="btn btn-success waves-effect waves-lightbotonAbajo"
                @click="agregarServicio"
              >
                Insertar Servicio
              </button>
            </div>
          </div>
          <div class="row mt-3">
            <ul class="list-group pe-0" v-show="listaServicios.length > 0">
              <li
                class="list-group-item d-flex justify-content-between align-items-center"
                v-for="serv in listaServicios"
                :key="serv.id"
              >
                <span>
                  <span
                    class="badge bg-danger rounded-pill pointer"
                    v-show="serv.nuevo == 1"
                    @click="deleteServicioLista(serv)"
                    ><i class="far fa-1x fa-trash-can"></i
                  ></span>
                  {{ serv.nombre }}
                </span>

                <span class="badge bg-primary rounded-pill text-dark">
                  <span
                    class="badge bg-dark text-primary rounded-pill pointer"
                    v-show="serv.garantia_id"
                    >Garantia</span
                  >
                  $ {{ serv.precio }}</span
                >
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="row text-center my-5" v-if="props.getOrden.estado < 5">
        <div class="col-12">
          <button
            class="btn btn-success waves-effect waves-light"
            @click="guardarDiagnostico(diagnostico.id_estado)"
          >
            Guardar Diagnóstico y Servicios
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.loader {
  text-align: center;
  color: #bbbbbb;
}
.botonAbajo {
  vertical-align: text-bottom;
}
.pointer {
  cursor: pointer;
}
</style>
