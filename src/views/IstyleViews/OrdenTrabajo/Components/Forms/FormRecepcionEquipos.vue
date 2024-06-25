<script setup>
import { computed, onBeforeMount, reactive, ref } from "vue";
import moment from "moment";
import Swal from "sweetalert2";
import axios from "axios";

const rutaAPI = import.meta.env.VITE_URL_API;

let equipos = ref();
let modelos = ref();

const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
onBeforeMount(() => {
  axios
    .get(rutaAPI + "equipos", token)
    .then(function (response) {
      equipos.value = response.data.equipos;
    })
    .catch(function (error) {
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
    });
  axios
    .get(rutaAPI + "modelos", token)
    .then(function (response) {
      modelos.value = response.data.modelo;
    })
    .catch(function (error) {
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
    });
});

const orden = reactive({
  fehca_actual: moment(new Date()).format("YYYY-MM-D"),
  fehca_entrega: null,
  equipo: null,
  modelo: null,
  run: null,
  nombre: null,
  email: null,
  fono: null,
  imei: null,
  serie: null,
  valor_diagnostico: 19990,
});

async function searchCliente() {
  if (!orden.run) {
    Swal.fire({
      title: "Error run invalido!",
      text: "Debe ingresar un run valido!",
      icon: "error",
      confirmButtonText: "OK",
    });
    return;
  }
  axios
    .get(rutaAPI + "clientes/run/" + orden.run, token)
    .then(function (response) {
      // handle success
      orden.nombre = response.data.nombre;
      orden.email = response.data.mail;
      orden.fono = response.data.fono;
      console.log(response);
    })
    .catch(function (error) {
      // handle error
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
    });
}

const getModelos = computed(() => {
  if (!orden.equipo) {
    return modelos.value;
  }
  return modelos.value.filter((item) => item.modelo === orden.equipo);
});
</script>

<template>
  <div class="card-body">
    <p class="card-text"></p>
    <div class="row">
      <div class="col">
        <div class="row">
          <div class="col"><label class="label-control">Run:</label></div>
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
              v-model="orden.run"
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
          type="date"
          label="fecha Ingreso"
          v-model="orden.fehca_actual"
          name="fecha"
          class="form-control form-control-sm"
          wfd-id="id5"
        />
      </div>
    </div>
    <div class="row">
      <div class="col">
        <label class="label-control">Nombre:</label>
        <input
          label="nombre"
          name="nombre"
          placeholder="nombre"
          id="nombre"
          v-model="orden.nombre"
          class="form-control form-control-sm"
          wfd-id="id7"
        />
      </div>
      <div class="col">
        <label class="label-control">Mail:</label>
        <input
          type="mail"
          label="Mail"
          v-model="orden.email"
          name="mail"
          placeholder="Mail"
          success-text="Run Correcto"
          class="form-control form-control-sm"
          wfd-id="id10"
        />
      </div>
      <div class="col">
        <label class="label-control">Contacto:</label>
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
            v-model="orden.fono"
            class="form-control form-control-sm"
            wfd-id="id6"
          />
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <label class="label-control">Equipo:</label>
        <select class="form-control form-control-sm" v-model="orden.equipo">
          <option value="null">Seleccionar..</option>
          <option v-for="equipo in equipos" :key="equipo.id" :value="equipo.id">
            {{ equipo.nombre }}
          </option>
        </select>
      </div>
      <div class="col">
        <label class="label-control">Modelo:</label>
        <input type="hidden" name="" wfd-id="id9" />
        <select class="form-control form-control-sm" v-model="orden.modelo">
          <option value="null">Seleccionar..</option>
          <option
            v-for="modelo in getModelos"
            :key="modelo.id"
            :value="modelo.id"
          >
            {{ modelo.nombre }}
          </option>
        </select>
      </div>
      <div class="col">
        <label class="label-control">IMEI:</label>
        <input
          label="IMEI"
          type="number"
          name="imei"
          placeholder="Imei"
          class="form-control form-control-sm"
          v-model="orden.imei"
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
        <label class="label-control">Serie:</label>
        <input
          label="RUN"
          placeholder="serie"
          name="serie"
          success-text="Run Correcto"
          class="form-control form-control-sm"
          v-model="orden.serie"
        />
      </div>

      <div class="col">
        <input type="hidden" name="id_cliente" id="id_cliente" wfd-id="id13" />
        <label class="label-control">Valor Diagnostico:</label>
        <div class="input-group">
          <div class="input-group-prepend">
            <div class="input-group-text">$</div>
          </div>
          <input
            type="number"
            label="RUN"
            placeholder="0"
            name="serie"
            success-text="Run Correcto"
            class="form-control form-control-sm"
            v-model="orden.valor_diagnostico"
          />
        </div>
      </div>

      <div class="col">
        <label class="label-control">Fecha Entrega:</label>
        <input
          type="date"
          label="fecha Entrega"
          placeholder="fecha entrega"
          name="fechaentrega"
          class="form-control form-control-sm"
          wfd-id="id8"
        />
      </div>
    </div>
  </div>
</template>

<style></style>
