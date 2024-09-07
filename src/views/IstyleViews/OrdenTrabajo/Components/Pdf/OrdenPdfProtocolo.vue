<script setup>
import { onMounted, reactive, ref } from "vue";
import { useRoute } from "vue-router";
import moment from "moment";
import axios from "axios";

const route = useRoute();
const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const printObj = {
  id: "printOTN",
  popTitle: "ORDEN DE TRABAJO",
  extraHead: '<meta http-equiv="Content-Language"content="zh-cn"/>',
};

const dataOrden = reactive({
  nombre: null,
  run: null,
  fono: null,
  email: null,
  equipo: null,
  modelo: null,
  imei: null,
  codigo: null,
  valor: null,
  tecnico: null,
  entrega: "Sin fecha",
  ingreso: null,
  obs: null,
  estado_dispositivo: null,
});

const respuestaOrden = ref();

onMounted(() => {
  axios
    .get(rutaAPI + "ordenes/" + route.query.idOrden, token)
    .then((response) => {
      dataOrden.nombre = response.data.orden.Cliente.nombre;
      dataOrden.run = response.data.orden.Cliente.run;
      dataOrden.fono = response.data.orden.Cliente.fono;
      dataOrden.email = response.data.orden.Cliente.mail;
      dataOrden.equipo = response.data.orden.Dispositivo.nombre;
      dataOrden.modelo = response.data.orden.Equipo.nombre;
      dataOrden.valor = response.data.orden.valor;
      dataOrden.tecnico = response.data.orden.tecnico;
      dataOrden.imei = response.data.orden.imei;
      dataOrden.codigo = response.data.orden.codigo;
      dataOrden.obs = response.data.orden.observacion;
      //Falto definir estado del dispositivo
      dataOrden.estado_dispositivo = response.data.orden.estado_dispositivo;
      if (response.data.orden.fecha_entrega)
        dataOrden.entrega = moment(response.data.orden.fecha_entrega).format(
          "DD-MM-YYYY"
        );
      dataOrden.ingreso = moment(response.data.orden.created_at).format(
        "DD-MM-YYYY HH:mm"
      );
      respuestaOrden.value = response.data.orden.respuestas;
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>
<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="text-end">
          <button
            type="button"
            id="btnPrintIS"
            class="btn btn-primary mb-3 waves-effect waves-light"
            v-print="printObj"
          >
            Imprimir Orden de Trabajo
          </button>
        </div>
        <div class="card" id="printOTN">
          <h5 class="card-header"></h5>
          <div class="card-body">
            <div class="row mt-3">
              <div class="container">
                <div class="col-12">
                  <div class="row">
                    <div class="col-3">
                      <img
                        src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAu4AAADTCAYAAADeZpaQAAABgWlDQ1BIRCA3MDktQQAAKJGVjj9rWmEUh59XTUxRqARpHUp5IaV0uAZjB6vJ4h+ohgxiW1C36/VGA1d9ub5i8gGyZUmG0C4tbb9CSZYMGUOGZAgUCtLPUBACpYTb4ZI6hdDf9JwHzjk/CGhTKScE9Prarb0uyHqjKcMTIkRZJMdj0xqqfLW6wZ25/o4AuEqaSjmbld8/1nbHn77Nr394mtPG3XsARNr20AKxAFjtodUD4QCGpVwN4j2QHGulQZwBcbfeaIKYAPGOz7+AeKveaEIgBMTdt7UiBBJArOXzCyDW8fkVELO6ZhsCZcDwOwDwoFySmVQ2mb+n93+n54xufwggavffvQFiwBPKlJBkSJElSV7b2xqgOFA77lanq2VeKceWxUFPjbTtGrLSt5YNmU6tpADqjab0T09rCEA8upy5wWfILkFwb+Zah3B8AonzmXv2ER6uwtGFMl3zX3FxHbpvHm6+TPscLcDcT8+bPofwAdzse96fL5538xWCEzh1/gIkd2ngdRvKIgAAAAlwSFlzAAA2wAAANsAB2yLWFAAABsBpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMTQ1IDc5LjE2MzQ5OSwgMjAxOC8wOC8xMy0xNjo0MDoyMiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1sbnM6ZGM9Imh0dHA6Ly9wdXJsLm9yZy9kYy9lbGVtZW50cy8xLjEvIiB4bWxuczpwaG90b3Nob3A9Imh0dHA6Ly9ucy5hZG9iZS5jb20vcGhvdG9zaG9wLzEuMC8iIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIDIxLjAgKE1hY2ludG9zaCkiIHhtcDpDcmVhdGVEYXRlPSIyMDIwLTAxLTIxVDEwOjE1OjUyLTAzOjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTAyLTI1VDAyOjU0OjEwLTAzOjAwIiB4bXA6TW9kaWZ5RGF0ZT0iMjAyMC0wMi0yNVQwMjo1NDoxMC0wMzowMCIgeG1wTU06SW5zdGFuY2VJRD0ieG1wLmlpZDpiNmRlMDc1Yi00YTVkLTRkMjMtOTU4YS0xMDQ2YjIyYmNkOGIiIHhtcE1NOkRvY3VtZW50SUQ9ImFkb2JlOmRvY2lkOnBob3Rvc2hvcDo3NzYyNTAxNi04YzMyLWQzNDItYWNiYi05ZDJmYTUwMTE1MjQiIHhtcE1NOk9yaWdpbmFsRG9jdW1lbnRJRD0ieG1wLmRpZDo1YTc2OGMzNy1hMzIxLTQwMGUtYjI2Ny02YjA5MTE4OGY4MmMiIGRjOmZvcm1hdD0iaW1hZ2UvcG5nIiBwaG90b3Nob3A6Q29sb3JNb2RlPSIzIiBwaG90b3Nob3A6SUNDUHJvZmlsZT0iSEQgNzA5LUEiPiA8eG1wTU06SGlzdG9yeT4gPHJkZjpTZXE+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJjcmVhdGVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOjVhNzY4YzM3LWEzMjEtNDAwZS1iMjY3LTZiMDkxMTg4ZjgyYyIgc3RFdnQ6d2hlbj0iMjAyMC0wMS0yMVQxMDoxNTo1Mi0wMzowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIDIxLjAgKE1hY2ludG9zaCkiLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249InNhdmVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOmMxNTBmOGVjLTY2OTItNDZhZC04YzQwLTc2MWY1ODQzZGRlZSIgc3RFdnQ6d2hlbj0iMjAyMC0wMS0yMVQxMDox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"
                        width="80%"
                        alt=""
                      />
                    </div>
                    <div class="col-6 pr-0">
                      <h5 style="font-size: 12px; margin-bottom: 5px">
                        Misael Enrique Sobrevia Rodríguez E.I.R.L.
                      </h5>
                      <h3 style="font-size: 12px; margin-bottom: 5px">
                        RUT: 76.325.738-K
                      </h3>
                      <h4 style="font-size: 12px; margin-bottom: 5px">
                        Bolognesi #340 Boulevard Vereda Bolognesi Local 2 & 18
                      </h4>
                      <h5 style="font-size: 12px; margin-bottom: 5px">
                        <i class="fa fa-at"></i> support@istylestore.cl -
                        <i class="fa fa-globe"></i> www.istylestore.cl
                      </h5>
                      <h5 style="font-size: 12px; margin-bottom: 5px">
                        <i aria-hidden="true" class="fa fa-phone-square"></i>
                        +56 9 56333621 -
                        <i aria-hidden="true" class="fa fa-phone-square"></i> 58
                        2 498666
                      </h5>
                    </div>
                    <div class="col-3 text-center">
                      <h3>ORDEN DE TRABAJO</h3>
                      <p class="numeroOTp">{{ route.query.idOrden }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="col-12">
                <div
                  class="card mb-3"
                  style="
                    background-color: #d3d3d3;
                    border-radius: 10px;
                    -webkit-print-color-adjust: exact;
                  "
                >
                  <div class="card-body">
                    <div class="row">
                      <div class="col-3">
                        <div class="form-inline">
                          <p>Nombre:</p>
                          <input
                            v-model="dataOrden.nombre"
                            class="form-control"
                            type="text"
                          />
                        </div>
                        <div class="form-inline">
                          <p>Equipo:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.equipo"
                            type="text"
                          />
                        </div>
                      </div>
                      <div class="col-3">
                        <div class="form-inline">
                          <p>Rut:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.run"
                            type="text"
                          />
                        </div>
                        <div class="form-inline">
                          <p>Modelo:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.modelo"
                            type="text"
                          />
                        </div>
                      </div>
                      <div class="col-3">
                        <div class="form-inline">
                          <p>Telefono:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.fono"
                            type="text"
                          />
                        </div>
                        <div class="form-inline">
                          <p>Imei:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.imei"
                            type="text"
                          />
                        </div>
                      </div>
                      <div class="col-3">
                        <div class="form-inline">
                          <p>E-mail:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.email"
                            type="text"
                          />
                        </div>
                        <div class="form-inline">
                          <p>Código Acceso:</p>
                          <input
                            class="form-control"
                            v-model="dataOrden.codigo"
                            type="text"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-3">
              <div class="container">
                <div class="col-12">
                  <div class="row">
                    <div class="col-6">
                      <div class="row">
                        <div class="col-9">
                          <b style="font-size: 12px"
                            >¿el equipo se encuentra encendido?</b
                          >
                        </div>
                        <div class="col-2 mt-1 text-center">
                          <div
                            style="font-size: 12px"
                            v-show="dataOrden.estado_dispositivo == 1"
                            class="btnVerde"
                          >
                            SI
                          </div>
                          <div
                            style="font-size: 12px"
                            v-show="dataOrden.estado_dispositivo == 2"
                            class="btnRojo"
                          >
                            No
                          </div>
                          <div
                            style="font-size: 12px"
                            v-show="dataOrden.estado_dispositivo == 3"
                            class="btnRojo"
                          >
                            Bloqueado
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="col-12 mt-1">
                  <div class="row">
                    <div
                      class="col-6 mt-2"
                      v-for="respuesta in respuestaOrden"
                      :key="respuesta.id"
                    >
                      <div class="row">
                        <div class="col-9">
                          <label style="font-size: 12px"
                            ><b>{{ respuesta.pregunta.descripcion }}</b>
                            <b
                              style="
                                font-size: 12px;
                                background-color: #25303f;
                                border-radius: 4px;
                                padding: 2px 5px;
                                margin-left: 5px;
                                color: white;
                              "
                              v-show="respuesta.respuesta"
                              >{{ respuesta.respuesta }}</b
                            >
                          </label>
                        </div>

                        <div class="col-3 text-center">
                          <div
                            class="btnVerde"
                            style="
                              -webkit-print-color-adjust: exact;
                              font-size: 10px;
                            "
                            v-show="respuesta.check_resp"
                          >
                            Si
                          </div>
                          <div
                            class="btnRojo"
                            style="
                              -webkit-print-color-adjust: exact;
                              font-size: 10px;
                            "
                            v-show="!respuesta.check_resp"
                          >
                            No
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="card w-100 border-0 mb-2">
                <div class="card-body areatext mx-4 py-0">
                  <div class="row">
                    <div class="col-6" style="border-right: 5px solid #26e2bd">
                      <textarea
                        class="border-0 w-100 pl-2 pt-1 mt-2"
                        rows="3"
                        v-model="dataOrden.obs"
                      ></textarea>
                    </div>
                    <div class="col-3 text-center" style="align-self: flex-end">
                      <p>Firma</p>
                    </div>
                    <div
                      class="col-3"
                      style="
                        border-left: 5px solid #26e2bd;
                        display: flex;
                        justify-content: center;
                        align-items: center;
                      "
                    >
                      <h2>
                        {{ dataOrden.valor }}
                      </h2>
                    </div>
                  </div>
                </div>

                <div class="card-body">
                  <div class="row ml-2">
                    <div class="col-4">
                      <div style="font-size: 14px">
                        Nombre del Tecnico:
                        {{ dataOrden.tecnico }}
                      </div>
                    </div>
                    <div class="col-4">
                      <div style="font-size: 14px">
                        Fecha de Ingreso: {{ dataOrden.ingreso }}
                      </div>
                    </div>
                    <div class="col-4">
                      <div style="font-size: 14px">
                        Fecha acordada de Entrega:
                        {{ dataOrden.entrega || "Sin fecha" }}
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-12 text-right">
                <img
                  src="data:image/png;base64,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"
                  width="80"
                  alt=""
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style type="text/css" scoped>
@media print {
  header {
    display: none;
  }
  footer {
    display: none;
  }
}
.form-control {
  font-size: 10px !important;
}
#btnPrintIS {
  background-color: #25303f !important;
  color: #45dabe;
  border-color: #45dabe !important;
}
#btnPrintIS:hover {
  color: #fff;
  background-color: #227dc7;
  border-color: #2176bd;
  box-shadow: 0 8px 25px -8px #45dabe;
}

.tblrec {
  border: 2px solid;
  background-color: #d3d3d3;
}
.mt-6 {
  margin-top: 4rem !important;
}
.mt-7 {
  margin-top: 5.8rem !important;
}
hr {
  height: 10px;
  width: 50%;
  background-color: black;
  margin-bottom: 0.5rem !important;
}
.btnVerde {
  -webkit-print-color-adjust: exact;
  background-color: #26e2bd;
  border-radius: 40px !important;
  padding: 5px 15px;
  width: 55px;
}
.btnRojo {
  -webkit-print-color-adjust: exact;
  background-color: rgb(238, 75, 75);
  color: #000;
  border-radius: 40px !important;
  padding: 5px 15px; /* Ajusta el padding según tus necesidades */
  display: inline-block; /* Asegura que el botón se ajuste al tamaño del contenido */
  text-align: center;
}

.brtl-30 {
  border-top-left-radius: 30px;
}
.bl-5st {
  border-left: 5px solid #26e2bd;
}
#pagosOT tbody tr td:nth-last-child(1) {
  border-left: 5px solid #26e2bd;
}
#pagosOT tbody tr td:nth-last-child(3) {
  border-right: 5px solid #26e2bd;
}
.brrl-30 {
  border-top-right-radius: 30px;
}
#firmaOT {
  border: 5px solid #26e2bd;
  border-bottom-left-radius: 40px;
  border-bottom-right-radius: 40px;
}
#pagosOT {
  border-collapse: separate !important;
  border-spacing: 0;
  border: 5px solid #26e2bd;
  border-top-left-radius: 40px;
  border-top-right-radius: 40px;
}
#pagosOT thead {
  border-collapse: collapse;
  background-color: #26e2bd;
}
#pagosOT th {
  color: white;
  padding-bottom: 10px !important;
  padding-top: 10px !important;
  font-weight: bold !important;
  background: none !important;
}
p {
  margin-bottom: 0.3rem !important;
  font-size: 0.8rem !important;
}
.form-inline p {
  margin-right: 5px;
  font-weight: 600;
}
.form-inline input {
  border-radius: 20px;
  margin-bottom: 1rem !important;
}
h5 {
  font-weight: 600 !important;
}
img {
  margin-top: 20px !important;
  margin-left: 10px !important;
}
.numeroOTp {
  font-size: 2.5rem !important;
  margin-top: 1rem !important;
  background: #26e2bd !important;
  padding: 8px 15px !important;
  color: white !important;
  border-radius: 20px !important;
  margin: 0 auto !important;
  -webkit-print-color-adjust: exact;
}
.numeroOT h3 {
  margin-top: 2rem !important;
}
.rect {
  border: 8px solid #d3d3d3;
  width: 100%;
  height: 190px;
  border-radius: 20px;
}
.areatext {
  border: 5px solid #26e2bd;
  border-radius: 40px;
}

.areatext2 {
  border: 5px solid #26e2bd;
  border-radius: 0px 0px 40px 40px;
}
.areatext3 {
  border: 5px solid #26e2bd;
  border-radius: 0px 0px 0px 0px;
}
</style>
