<script setup>
import FormPreguntas from "./Components/Forms/FormPreguntas.vue";
import { computed, onBeforeMount, onMounted, reactive, ref } from "vue";
import { useRouter } from "vue-router";
import moment from "moment";
import Swal from "sweetalert2";
import axios from "axios";

const rutaAPI = import.meta.env.VITE_URL_API;
const router = useRouter();
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const equipos = ref();
const modelos = ref();
const estados = ref();
const equipos_preguntas = ref();

const isModalOpened = ref(false);

const openModal = () => {
  console.log("abrir modal");
  isModalOpened.value = true;
};

const closeModal = () => {
  isModalOpened.value = false;
};
const nuevoEquipo = reactive({
  selected_idEquipo: null,
  nombreEquipo: null,
  nombreModelo: null,
});
const orden = reactive({
  fecha_entrega: null,
  tecnico: localStorage.getItem("Nombre"),
  cliente_id: null,
  imei: null,
  codigo: null,
  id_equipo: null,
  id_dispositivo: null,
  observacion: null,
  estado_dispositivo: null,
  estado: 1,
  total_recepcion: 19990,
  total: 0,
  created_at: moment().format("YYYY-MM-DDTHH:mm"),
});
const cliente = reactive({
  run: null,
  nombre: null,
  mail: null,
  fono: null,
  existe: null,
});

onBeforeMount(() => {
  axios.get(rutaAPI + "equipos", token).then(function (response) {
    equipos.value = response.data.equipos;
  });
  axios.get(rutaAPI + "modelos", token).then(function (response) {
    modelos.value = response.data.modelo;
  });
  axios.get(rutaAPI + "estados", token).then(function (response) {
    estados.value = response.data.estados;
  });
});

onMounted(() => {
  axios.get(rutaAPI + "equipo_preguntas", token).then(function (response) {
    equipos_preguntas.value = response.data.preguntas.map((item) => {
      item.respuesta = null;
      item.check_resp = true;
      return item;
    });
  });
});

async function searchCliente() {
  if (!cliente.run) {
    Swal.fire({
      title: "Error run invalido!",
      text: "Debe ingresar un run valido!",
      icon: "error",
      confirmButtonText: "OK",
    });
    return;
  }
  await axios
    .get(rutaAPI + "clientes/run/" + cliente.run, token)
    .then(function (response) {
      if (response.data) {
        cliente.nombre = response.data.nombre;
        cliente.mail = response.data.mail;
        cliente.fono = response.data.fono;
        cliente.existe = true;
        orden.cliente_id = response.data.id;
      }
    })
    .catch(function (error) {
      Swal.fire({
        title: "Info!",
        text: error.response.data.msg,
        icon: "info",
        confirmButtonText: "OK",
      });
      cliente.nombre = null;
      cliente.mail = null;
      cliente.fono = null;
      cliente.existe = null;
    });
}

async function sendData() {
  if (
    !cliente.run ||
    !cliente.nombre ||
    !orden.id_equipo ||
    !cliente.fono ||
    !orden.id_dispositivo ||
    !orden.estado_dispositivo
  ) {
    Swal.fire({
      title: "Error campos imcompletos!",
      text: "Debe ingresar un valor valido para todos los campos marcados con (*)!",
      icon: "error",
      confirmButtonText: "OK",
    });
    return;
  }

  if (!cliente.existe) {
    const cliente_bd = await axios.post(rutaAPI + "clientes", cliente, token);
    orden.cliente_id = cliente_bd.data.id;
  }

  if (orden.cliente_id) {
    cliente.existe = true;
    let respuestas = [];
    //Cargar valor de recepcion cuando se crea una nueva orden
    // orden.total_recepcion = orden.total;
    await axios
      .post(rutaAPI + "ordenes", orden, token)
      .then(function (response) {
        if (response.data.id) {
          let valores = Object.values(getPreguntas.value); // valores = ["Scott", "Negro", true, 5];
          for (let i = 0; i < valores.length; i++) {
            let params = {
              pregunta_id: valores[i].id_pregunta,
              respuesta: valores[i].respuesta,
              orden_id: response.data.id,
              check_resp: valores[i].check_resp,
            };
            respuestas.push(params);
          }
          axios
            .post(rutaAPI + "respuestas", respuestas, token)
            .then(function (resp) {
              if (resp) {
                Swal.fire({
                  title: "Excelente!",
                  text:
                    "Orden Nº " +
                    response.data.id +
                    " ingresada correctamente!",
                  icon: "success",
                  confirmButtonText: "OK",
                });
                router.push({
                  name: "ordenprotocolo",
                  query: { idOrden: response.data.id },
                });
              }
            });
        }
      });
  }
}

const getModelos = computed(() => {
  if (!orden.id_equipo) {
    return modelos.value;
  }
  return modelos.value.filter((item) => item.modelo === orden.id_equipo);
});

let getPreguntas = computed(() => {
  if (
    orden.estado_dispositivo !== null &&
    orden.id_equipo !== null &&
    orden.id_dispositivo !== null
  ) {
    return equipos_preguntas.value.filter((item) => {
      return (
        item.id_equipo === orden.id_equipo &&
        item.estado === orden.estado_dispositivo
      );
    });
  } else {
    return null;
  }
});

function onlyNumber(e) {
  const invalidChars = ["-", "+", "e"];
  if (invalidChars.includes(e.key)) {
    e.preventDefault();
  }
}

function Checks(data) {
  getPreguntas.value[
    getPreguntas.value.indexOf(
      getPreguntas.value.find((gP) => gP.id_pregunta == data.id)
    )
  ].check_resp = data.checked;
}
function textChecks(data) {
  getPreguntas.value[
    getPreguntas.value.indexOf(
      getPreguntas.value.find((gP) => gP.id == data.id)
    )
  ].respuesta = data.texto;
}
async function addEquipooModelo() {
  console.log("entro metodo");
  if (nuevoEquipo.selected_idEquipo && nuevoEquipo.nombreModelo != "") {
    let params = {
      nombre: nuevoEquipo.nombreModelo,
      modelo: nuevoEquipo.selected_idEquipo,
    };
    if (nuevoEquipo.selected_idEquipo == "otro") {
      await axios
        .post(rutaAPI + "equipos", { nombre: nuevoEquipo.nombreEquipo }, token)
        .then((response) => {
          params.modelo = response.data.id;
          equipos.value.push(response.data);
          orden.id_equipo = response.data.id;
        });
    }
    await axios.post(rutaAPI + "modelos", params, token).then((response) => {
      getModelos.value.push(response.data);
      Swal.fire({
        title: "Excelente!",
        text: " Datos ingresados correctamente!",
        icon: "success",
        confirmButtonText: "OK",
      });
      closeModal();
      orden.id_dispositivo = response.data.id;
    });
  }
}
</script>

<template>
  <!-- Page Content -->
  <div class="content">
    <BaseBlock title="Protocolo de recepción de equipos">
      <div class="card-body mb-3">
        <p class="card-text"></p>
        <div class="row">
          <div class="col">
            <div class="row">
              <div class="col">
                <label class="label-control">Run: <span>*</span></label>
              </div>
            </div>
            <div class="row">
              <div class="col">
                <input
                  type="search"
                  label="RUN"
                  placeholder="RUN ejemplo(12345678-9)"
                  name="run"
                  success-text="Run Correcto"
                  class="form-control form-control-sm"
                  wfd-id="id3"
                  v-model="cliente.run"
                />
              </div>
              <div class="col-3">
                <button
                  class="btn btn-dark waves-effect waves-light"
                  @click="searchCliente"
                >
                  Buscar
                </button>
              </div>
            </div>
          </div>
          <div class="col-md"></div>
          <div class="col-md-3">
            <label class="label-control">Fecha Ingreso:</label>
            <input
              type="datetime-local"
              label="fecha Ingreso"
              v-model="orden.created_at"
              class="form-control form-control-sm"
              wfd-id="id5"
            />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <label class="label-control">Nombre: <span>*</span></label>
            <input
              label="nombre"
              name="nombre"
              placeholder="nombre"
              id="nombre"
              v-model="cliente.nombre"
              class="form-control form-control-sm"
              wfd-id="id7"
            />
          </div>
          <div class="col">
            <label class="label-control">Mail:</label>
            <input
              type="mail"
              label="Mail"
              v-model="cliente.mail"
              name="mail"
              placeholder="Mail"
              success-text="Run Correcto"
              class="form-control form-control-sm"
              wfd-id="id10"
            />
          </div>
          <div class="col">
            <label class="label-control">Contacto: <span>*</span></label>
            <div class="input-group">
              <div class="input-group-prepend">
                <div class="input-group-text">+569</div>
              </div>
              <input
                type="number"
                size="8"
                maxlength="8"
                oninput="if(this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
                placeholder="Contacto"
                name="fono"
                v-model="cliente.fono"
                class="form-control form-control-sm"
                wfd-id="id6"
              />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <label class="label-control">Equipo: <span>*</span></label>
            <div class="input-group">
              <select
                class="form-control form-control-sm"
                v-model="orden.id_equipo"
              >
                <option :value="null">Seleccionar...</option>
                <option
                  v-for="equipo in equipos"
                  :key="equipo.id"
                  :value="equipo.id"
                >
                  {{ equipo.nombre }}
                </option>
              </select>
              <div class="input-group-prepend pointer">
                <div
                  class="input-group-text bg-dark text-primary"
                  @click="openModal()"
                >
                  +
                </div>
              </div>
            </div>
          </div>
          <div class="col">
            <label class="label-control">Modelo: <span>*</span></label>

            <div class="input-group">
              <input type="hidden" name="" wfd-id="id9" />
              <select
                class="form-control form-control-sm"
                v-model="orden.id_dispositivo"
              >
                <option :value="null">Seleccionar...</option>
                <option
                  v-for="modelo in getModelos"
                  :key="modelo.id"
                  :value="modelo.id"
                >
                  {{ modelo.nombre }}
                </option>
              </select>
              <div class="input-group-prepend pointer">
                <div
                  class="input-group-text bg-dark text-primary"
                  @click="openModal()"
                >
                  +
                </div>
              </div>
            </div>
          </div>
          <div class="col">
            <label class="label-control">Código:</label>
            <input
              label="RUN"
              placeholder="Codigo o clave de ingreso"
              name="serie"
              success-text="Run Correcto"
              class="form-control form-control-sm"
              v-model="orden.codigo"
            />
          </div>
        </div>
        <div class="row">
          <!-- <div class="col">
            <label class="label-control">Codigo:</label>
            <input
              label="codigo"
              placeholder="codigo"
              name="codigo"
              class="form-control form-control-sm"
              wfd-id="id11"
            />
          </div> -->
          <div class="col">
            <label class="label-control">IMEI o Serie:</label>
            <input
              label="IMEI"
              type="number"
              name="imei"
              placeholder="Imei o Serie"
              class="form-control form-control-sm"
              v-model="orden.imei"
              @keydown="onlyNumber"
            />
          </div>

          <div class="col">
            <label class="label-control">Valor Diagnostico:</label>
            <div class="input-group">
              <div class="input-group-prepend">
                <div class="input-group-text">$</div>
              </div>
              <input
                type="number"
                class="form-control form-control-sm"
                v-model="orden.total_recepcion"
              />
            </div>
          </div>
          <div class="col">
            <label class="label-control">Fecha Entrega:</label>
            <input
              type="date"
              label="fecha Entrega"
              placeholder="fecha entrega"
              v-model="orden.fecha_entrega"
              class="form-control form-control-sm"
              wfd-id="id8"
            />
          </div>
        </div>
      </div>
    </BaseBlock>
    <BaseBlock title="Estado del equipo">
      <div class="">
        <div class="card-body row">
          <div class="col-10">
            <div class="row">
              <div class="col-3">
                1.-En que estado ingresa el celular <span>*</span>
              </div>
              <div class="col-3">
                <select class="form-control" v-model="orden.estado_dispositivo">
                  <option :value="null">Seleccionar...</option>
                  <option
                    v-for="estado in estados"
                    :key="estado.id"
                    :value="estado.id"
                  >
                    {{ estado.nombre }}
                  </option>
                </select>
              </div>
            </div>
          </div>
          <div class="col-2"></div>
          <div class="col-12">
            <!-- Utilizamos v-if para condicionalmente renderizar el componente FormPreguntas -->
            <FormPreguntas
              :getPreguntas="getPreguntas"
              @custom-change="Checks"
              @text-change="textChecks"
            />
            <br />
            <label>Observacion</label>
            <textarea
              name="textarea"
              rows="4"
              v-model="orden.observacion"
              class="form-control mt-2 mb-5 large-textarea"
            ></textarea>
          </div>
        </div>
      </div>

      <div class="col-12 text-center mb-5">
        <button
          class="btn btn-lg btn-primary waves-effect waves-light"
          @click="sendData"
        >
          Guardar
        </button>
      </div>
    </BaseBlock>
  </div>
  <!-- END Page Content -->

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
          <slot name="header"> Agregar equipo </slot>
        </div>
        <div class="modal-body">
          <slot name="content">
            <div class="row">
              <div class="col-12">
                <label class="label-control">Equipo: <span>*</span></label>
                <div class="input-group">
                  <select
                    class="form-control form-control-sm"
                    v-model="nuevoEquipo.selected_idEquipo"
                  >
                    <option value="null">Seleccionar...</option>
                    <option
                      v-for="equipo in equipos"
                      :key="equipo.id"
                      :value="equipo.id"
                    >
                      {{ equipo.nombre }}
                    </option>
                    <option value="otro">Otro...</option>
                  </select>
                </div>
              </div>
              <div
                class="col-12"
                v-if="nuevoEquipo.selected_idEquipo == 'otro'"
              >
                <label class="label-control"
                  >Nuevo Equipo: <span>*</span></label
                >
                <input
                  type="text"
                  placeholder="nombre equipo"
                  v-model="nuevoEquipo.nombreEquipo"
                  class="form-control form-control-sm"
                />
              </div>
              <div class="col-12">
                <label class="label-control">Modelo: <span>*</span></label>
                <input
                  type="text"
                  placeholder="nombre modelo"
                  v-model="nuevoEquipo.nombreModelo"
                  class="form-control form-control-sm"
                />
              </div>
              <div class="col-12 text-end mt-3">
                <button
                  class="btn btn-dark text-primary"
                  @click="addEquipooModelo"
                >
                  Agregar
                </button>
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
.form-control {
  height: auto;
}
span {
  color: indianred;
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
  width: 40%;
  margin: 150px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}
.large-textarea {
  border: 1px solid #63c9ad !important;
  border-radius: 20px !important;
}
.pointer {
  cursor: pointer;
}
</style>
