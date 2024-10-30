<script setup>
// import FormRevisionDiagnostico from "./Components/Forms/FormRevisionDiagnostico.vue";
import { onMounted, reactive, ref, watch } from "vue";
import Swal from "sweetalert2";
import axios from "axios";
import { useRouter } from "vue-router";
import moment from "moment";
// import RevisionHistorialTable from "../Tables/RevisionHistorialTable.vue";
import FormRevisionDiagnostico from "./FormRevisionDiagnostico.vue";
// import FormRevisionProducto from "./FormRevisionProducto.vue";
// import { or } from "@vuelidate/validators";
const router = useRouter();
const props = defineProps(["idOrden"]);

const rutaAPI = import.meta.env.VITE_URL_API;
// const router = useRouter();

const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const datosBusqueda = reactive({
  id: null,
  nombre: null,
  run: null,
});
const cerrarOt = ref(null);
const allOrdenes = ref();
const orden = ref({
  id: null,
  Cliente: {
    run: null,
    nombre: null,
    mail: null,
    fono: null,
  },
  Equipo: {
    nombre: null,
  },
  Dispositivo: {
    nombre: null,
  },
  created_at: null,
  fecha_entrega: null,
  codigo: null,
  imei: null,
  estado: null,
  observacion: null,
  revisiones: [],
  subtotal: 0,
  iva: 0,
  descuento: 0,
  total: 0,
  stt: 0,
  orden_has_servicios: [],
  metodoPago: null,
  estados_ordene: {
    nombre_estado: null,
  },
  soloRevision: 0,
});
const isModalOpened = ref(false);

const openModal = () => {
  isModalOpened.value = true;
};
const closeModal = () => {
  isModalOpened.value = false;
};

const getGarantia = ref({
  subtotal: 0,
  iva: 0,
  descuento: 0,
  total: 0,
});

watch(
  () => orden.value.subtotal,
  (subtotal, prevSubtotal) => {
    if (subtotal !== prevSubtotal) {
      orden.value.total = subtotal - orden.value.descuento;
      orden.value.iva = Math.round(subtotal * 0.19);
      orden.value.stt = Math.round(orden.value.subtotal * 0.81);
      // getGarantia.value.total = orden.value.total;
      // getGarantia.value.iva = Math.round(subtotal * 0.19);
      // getGarantia.value.subtotal = subtotal;
      console.log("stt", orden.value.stt);
    }
  }
);
watch(
  () => orden.value.descuento,
  (descuento, prevDescuento) => {
    if (descuento !== prevDescuento) {
      orden.value.total = orden.value.subtotal - descuento;
      getGarantia.value.total = getGarantia.value.subtotal - descuento;
    }
  }
);

onMounted(() => {
  if (props.idOrden) {
    busqueda(props.idOrden);
  }
});
async function busqueda(id = null) {
  console.log("id_send", id);
  if (id) {
    datosBusqueda.id = id;
    console.log("id_orden", datosBusqueda.id);
  }
  if (datosBusqueda.id || datosBusqueda.run || datosBusqueda.nombre) {
    await axios
      .post(rutaAPI + "ordenes/buscarOrden", datosBusqueda, token)
      .then(function (response) {
        if (response.data.orden) {
          console.log("desde axios> ", response.data.orden);
          resetOrden();
          datosBusqueda.id = null;
          datosBusqueda.nombre = null;
          datosBusqueda.run = null;
          if (response.data.rows == 1) {
            cargarOrden(response.data.orden);
          } else {
            allOrdenes.value = response.data.orden;
            openModal();
          }
        } else {
          Swal.fire({
            title: "No hay datos!",
            text: "No se registran datos para la información ingresada!",
            icon: "warning",
            confirmButtonText: "OK",
          });
        }
      });
  } else {
    Swal.fire({
      title: "Error campos incompletos!",
      text: "Debe ingresar un valor valido en alguno de los campos!",
      icon: "error",
      confirmButtonText: "OK",
    });
  }
}

function cargarOrden(data) {
  console.log("data", data);
  if (isModalOpened.value) {
    closeModal();
  }
  data.created_at = moment(data.created_at).format("YYYY-MM-DD HH:mm");
  data.soloRevision = data.total;
  data.stt = data.subtotal;
  data.metodoPago = null;
  data.ordenServicios = [];
  if (data.orden_has_servicios && data.orden_has_servicios.length > 0) {
    data.orden_has_servicios.map((item) => {
      console.log("ordenServicios", item);
      let params = {
        id: item.servicio.id,
        nombre: item.servicio.nombre,
        nuevo: 0,
        precio: item.servicio.precio,
        garantia_id: item.garantia_id,
        tittle: item.servicio.nombre + " - " + item.servicio.precio,
      };
      data.ordenServicios.push(params);
    });
  }
  if (data.id_ultima_garantia && data.estado == 4) {
    axios
      .get(rutaAPI + "garantia/" + data.id_ultima_garantia, token)
      .then(function (response) {
        orden.value.subtotal = response.data.subtotal;
        orden.value.iva = response.data.iva;
        orden.value.descuento = response.data.descuento;
        orden.value.total = response.data.total;
        orden.value.metodoPago = null;
        console.log("entro a garantia", response.data);
      });
  }
  orden.value = data;
}

function resetOrden() {
  orden.value.id = null;
  orden.value.Cliente.run = null;
  orden.value.Cliente.nombre = null;
  orden.value.Cliente.mail = null;
  orden.value.Cliente.fono = null;
  orden.value.Equipo.nombre = null;
  orden.value.Dispositivo.nombre = null;
  orden.value.created_at = null;
  orden.value.fecha_entrega = null;
  orden.value.codigo = null;
  orden.value.imei = null;
  orden.value.estado = null;
  orden.value.orden_has_servicios = null;
  orden.value.ordenServicios = [];
}

function updateValores(valor) {
  console.log("valor", valor);
  console.log("antes", orden.value.subtotal);
  if (valor.op == 1) {
    let suma = valor.value + orden.value.subtotal;
    orden.value.subtotal = suma;
  } else {
    orden.value.subtotal -= valor.value;
    if (orden.value.subtotal == 0) {
      orden.value.subtotal = orden.value.soloRevision;
    }
  }
}

async function habilidarGarantia() {
  let data = {
    fecha: moment().format("YYYY-MM-DD"),
    orden_id: orden.value.id,
  };
  axios
    .post(rutaAPI + "garantia", data, token)
    .then((response) => {
      orden.value.id_ultima_garantia = response.data.id;
    })
    .then(async () => {
      await updateOrden(4);
      // await busqueda(orden.value.id);
    });
}

function updateOrden(nuevo_estado) {
  const dataOrden = ref();
  if (orden.value.estado == 4) {
    dataOrden.value = {
      estado: 5,
    };
  } else {
    orden.value.estado = nuevo_estado;
    dataOrden.value = orden.value;
  }

  if (nuevo_estado == 5) {
    orden.value.fecha_entrega = moment().format("YYYY-MM-DD");
  }
  console.log("dataOrden.value", dataOrden.value);
  axios
    .put(rutaAPI + "ordenes/" + orden.value.id, dataOrden.value, token)
    .then((response) => {
      Swal.fire({
        title: "Excelente!",
        text: "Datos almacenado correctamente!",
        icon: "success",
        confirmButtonText: "OK",
      });
      if (nuevo_estado == 5) {
        router.push({
          name: "ordenpdf",
          query: { idOrden: response.data.id },
        });
      } else {
        busqueda(orden.value.id);
      }
    });
}

function finalizarOrden() {
  if (orden.value.metodoPago) {
    cerrarOt.value = 5;
    console.log("finalizar_orden", orden.value);
    if (orden.value.estado == 4) {
      axios
        .put(
          rutaAPI + "garantia/" + orden.value.id_ultima_garantia,
          {
            subtotal: orden.value.subtotal - orden.value.iva,
            iva: orden.value.iva,
            descuento: orden.value.descuento,
            total: orden.value.total,
          },
          token
        )
        .then((response) => {
          console.log("putGarantia", response);
        });
    }
  } else {
    Swal.fire({
      title: "Faltan Datos!",
      text: "Seleccione un metodo de pago!",
      icon: "warning",
      confirmButtonText: "OK",
    });
  }
}

function abrirPDF(nameRoute) {
  router.push({
    name: nameRoute,
    query: { idOrden: orden.value.id },
  });
}
</script>

<template>
  <BaseBlock title="Buscar Orden de Trabajo">
    <div class="card-body mb-4">
      <div class="row">
        <div class="col-md-2">
          <input
            type="search"
            v-model="datosBusqueda.id"
            placeholder="ID ORDEN"
            class="form-control form-control-sm"
          />
          <div
            class="list-group country-list3"
            style="position: absolute"
          ></div>
        </div>
        <div class="col-md-4">
          <input
            type="search"
            v-model="datosBusqueda.run"
            placeholder="RUN"
            class="form-control form-control-sm"
          />
          <div
            class="list-group country-list3"
            style="position: absolute"
          ></div>
        </div>
        <div class="col-md-4">
          <input
            type="search"
            v-model="datosBusqueda.nombre"
            placeholder="NOMBRE"
            class="form-control form-control-sm"
          />
          <div
            class="list-group country-list3"
            style="position: absolute"
          ></div>
        </div>
        <div class="col-md-2 text-center">
          <button
            class="btn btn-dark waves-effect waves-light btn-search-revision"
            @click="busqueda()"
          >
            Buscar Ordenes
          </button>
        </div>
      </div>
    </div>
  </BaseBlock>
  <div v-show="orden.id">
    <BaseBlock title="Datos de Orden">
      <div class="card-body mb-4">
        <div class="row">
          <div class="col-8 text-center">
            <h2>Orden nº {{ orden.id }}</h2>
            <button
              type="button"
              v-if="orden.estado == 5"
              class="btn btn-dark text-primary text-start"
              @click="habilidarGarantia"
            >
              Habilitar Garantia
            </button>
          </div>
          <div class="col-4 text-end">
            <p>
              Estado:
              <span class="bg-info px-2 py-1 rounded text-white">
                {{ orden.estados_ordene.nombre_estado }}</span
              >
              <span class="ms-5 pointer" @click="abrirPDF('ordenprotocolo')">
                <i class="fa fa-2x fa-file-pdf"></i>
              </span>
              <span
                class="ms-5 pointer"
                v-if="orden.estado == 5"
                @click="abrirPDF('ordenpdf')"
              >
                <i class="fa fa-2x fa-file-pdf"></i>
              </span>
            </p>
          </div>
        </div>
        <div class="row mt-4">
          <div class="col-md-4">
            <label>Run:</label>
            <input
              type="text"
              readonly
              placeholder="RUN"
              v-model="orden.Cliente.run"
              success-text="Run Correcto"
              class="form-control form-control-sm"
            />
          </div>

          <div class="col-12 col-md-4">
            <label>Nombre:</label>
            <input
              label="nombre"
              v-model="orden.Cliente.nombre"
              placeholder="nombre"
              readonly
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-4">
            <label>Fecha Ingreso:</label>
            <input
              type="datetime-local"
              label="fecha Ingreso"
              id="fechaActual"
              v-model="orden.created_at"
              readonly="readonly"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-4">
            <label>Teléfono:</label>
            <input
              placeholder="Contacto"
              v-model="orden.Cliente.fono"
              readonly
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-4">
            <label>Mail:</label>
            <input
              type="mail"
              label="Mail"
              v-model="orden.Cliente.mail"
              placeholder="Mail"
              readonly
              success-text="Run Correcto"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-4">
            <label>Fecha Entrega:</label>
            <input
              type="date"
              placeholder="fecha entrega"
              readonly
              v-model="orden.fecha_entrega"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-3">
            <label>Equipo:</label>
            <input
              type="text"
              name=""
              v-model="orden.Equipo.nombre"
              readonly="readonly"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-3">
            <label>Modelo:</label>
            <input
              type="text"
              v-model="orden.Dispositivo.nombre"
              readonly="readonly"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-3">
            <label>Codigo:</label>
            <input
              label="codigo"
              placeholder="codigo"
              v-model="orden.codigo"
              readonly="readonly"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-12 col-md-3">
            <label>IMEI:</label>
            <input
              label="IMEI"
              v-model="orden.imei"
              placeholder="Imei"
              readonly
              class="form-control form-control-sm"
            />
          </div>
        </div>
      </div>
    </BaseBlock>

    <BaseBlock title="Historial de Orden" v-if="orden.revisiones">
      <!-- <RevisionHistorialTable :getRevisiones="orden.revisiones" /> -->
      <div class="row">
        <div class="col-md-12">
          <div class="table-responsive m-5">
            <table class="table table-striped">
              <thead class="bg-primary text-dark">
                <tr>
                  <th scope="col">Nº</th>
                  <th>Orden</th>
                  <th>Técnico</th>
                  <th>Estado</th>
                  <th>Diagnóstico</th>
                  <th>fecha</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(revision, i) in orden.revisiones"
                  :key="revision.id"
                >
                  <td>{{ i + 1 }}</td>
                  <td>{{ revision.orden_id }}</td>
                  <td>{{ revision.responsable }}</td>
                  <td>{{ revision.estados_ordene.nombre_estado }}</td>
                  <td>{{ revision.observacion }}</td>
                  <td>{{ moment(revision.created_at).format("L LT") }}</td>
                </tr>
                <tr v-if="orden.revisiones.length < 1">
                  <td colspan="6">No registra revisiones o díagnosticos.</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </BaseBlock>

    <BaseBlock title="Diagnosticos">
      <FormRevisionDiagnostico
        :updateEstado="cerrarOt"
        :getOrden="orden"
        @setValores="updateValores"
        @updateOrden="updateOrden"
      />
    </BaseBlock>

    <!--Cuando el estado es otro que no sea Garantia-->
    <BaseBlock title="Estado de Orden">
      <div class="row">
        <div class="col-12">
          <div class="card-body">
            <div class="row">
              <div class="col-md-4">
                <label
                  >Valor diagnóstico previsto en recepción del equipo:</label
                >
                <input
                  label="total_recepcion"
                  v-model="orden.total_recepcion"
                  readonly="readonly"
                  class="form-control form-control-sm"
                />
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col-12">
          <div class="card-body">
            <div class="row">
              <div class="col-md-3">
                <label>BRUTO:</label>
                <input
                  label="precio"
                  v-model="orden.stt"
                  readonly="readonly"
                  class="form-control form-control-sm"
                />
              </div>
              <div class="col-md-3">
                <label>IVA:</label>
                <input
                  type="text"
                  v-model="orden.iva"
                  readonly="readonly"
                  aria-describedby="basic-addon2"
                  class="form-control form-control-sm"
                />
              </div>
              <div class="col-md-3">
                <label>DESCUENTO:</label>
                <input
                  type="text"
                  v-model="orden.descuento"
                  aria-describedby="basic-addon2"
                  class="form-control form-control-sm"
                  :disabled="orden.estado == 5"
                />
              </div>
              <div class="col-md-3">
                <label>TOTAL:</label>
                <input
                  label="total"
                  v-model="orden.total"
                  readonly="readonly"
                  class="form-control form-control-sm"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-12 py-4">
        <div class="row justify-content-md-center">
          <div class="col-md-4">
            <select
              class="form-control form-control-sm"
              v-model="orden.metodoPago"
            >
              <option disabled :value="null">Seleccione metodo de pago</option>
              <option value="1">EFECTIVO</option>
              <option value="2">REDBANK</option>
            </select>
          </div>
          <div class="col-md-auto text-center">
            <button
              class="btn btn-dark waves-effect waves-light"
              @click="finalizarOrden"
              v-if="orden.estado < 5"
            >
              Finalizar
            </button>
          </div>
        </div>
      </div>
    </BaseBlock>
  </div>
  <!-- Modal -->
  <div v-if="isModalOpened" class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container" ref="target">
        <div class="text-end relative">
          <label
            class="btn btn-sm btn-circle absolute right-2 top-2"
            @click.stop="closeModal"
            >✕</label
          >
        </div>
        <div class="modal-header bg-dark text-primary">
          <slot name="header"> Ordenes Disponible </slot>
        </div>
        <div class="modal-body">
          <slot name="content">
            <div class="row">
              <div class="col-md-12">
                <div class="table-responsive">
                  <table class="table table-hover mb-0">
                    <thead>
                      <tr>
                        <th scope="col">ID</th>
                        <th>Estado</th>
                        <th>Run</th>
                        <th>Nombre</th>
                        <th>Equipo</th>
                        <th>Modelo</th>
                        <th>Fecha Ingreso</th>
                      </tr>
                    </thead>
                    <tbody class="fs-sm">
                      <tr
                        v-for="ord in allOrdenes"
                        :key="ord.id"
                        class="pointer"
                        @click="cargarOrden(ord)"
                      >
                        <td class="text-dark">
                          <strong>
                            <u>{{ ord.id }}</u>
                          </strong>
                        </td>
                        <td>{{ ord.estados_ordene.nombre_estado }}</td>
                        <td>{{ ord.Cliente.run }}</td>
                        <td>{{ ord.Cliente.nombre }}</td>
                        <td>{{ ord.Equipo.nombre }}</td>
                        <td>{{ ord.Dispositivo.nombre }}</td>
                        <td>{{ moment(ord.created_at).format("L LT") }}</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </slot>
        </div>
        <div class="modal-footer">
          <slot name="footer">
            <div>
              <!-- <button @click.stop="closeModal">Submit</button> -->
              <!-- <button>Submit</button> -->
            </div>
          </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@media only screen and (max-width: 600px) {
  input[type="search"] {
    margin-top: 5px;
  }
  .btn-search-revision {
    margin-top: 10px;
  }
}
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}
.modal-container {
  width: 70%;
  margin: 150px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}
.pointer {
  cursor: pointer;
}
</style>
