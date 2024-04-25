<script setup></script>

<template>
  <div class="row">
    <div class="col-6">
      <div class="">
        <div class="card-body">
          <div class="row">
            <div class="col-4"><label>Buscar Producto:</label></div>
            <div class="col-6">
              <div class="frmSearch">
                <input
                  type="text"
                  name="search-box"
                  class="form-control form-control-sm"
                />
                <ul id="country-list"></ul>
              </div>
            </div>
            <div class="col-2">
              <button class="btn btn-dark waves-effect waves-light">
                Buscar
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-6">
      <div class="">
        <div class="card-body">
          <div class="row">
            <div class="col-4"><label>Agregar Servicio:</label></div>
            <div class="col-6">
              <input
                type="search"
                name=""
                class="form-control form-control-sm"
              />
              <ul id="country-list2"></ul>
            </div>
            <div class="col-2">
              <button class="btn btn-dark waves-effect waves-light">
                Buscar
              </button>
              <div class="form-check">
                <input
                  type="checkbox"
                  id="defaultCheck1"
                  class="form-check-input"
                />
                <label for="defaultCheck1" class="form-check-label">
                  Agregar Manual
                </label>
              </div>
            </div>
            <div class="card">
              <div class="card-content">
                <div class="card-body">
                  <h4 class="card-title">DETALLE DEL SERVICIO</h4>
                </div>
              </div>
              <!---->
              <div class="col-12 mb-4">
                <p>
                  SERVICIO :
                  <span
                    ><input type="text" name="" class="form-control"
                  /></span>
                </p>
                <p>
                  PRECIO : $
                  <span
                    ><input type="text" name="" class="form-control"
                  /></span>
                </p>
                <fieldset>
                  <div class="input-group">
                    <div
                      style="
                        display: flex;
                        justify-content: center;
                        align-items: center;
                      "
                    >
                      CANTIDAD :
                    </div>
                    <input
                      type="text"
                      placeholder="100"
                      aria-describedby="button-addon2"
                      class="form-control ml-2"
                    />
                    <div id="button-addon2" class="input-group-append">
                      <button
                        type="button"
                        class="btn btn-dark waves-effect waves-light"
                      >
                        Agregar
                      </button>
                    </div>
                  </div>
                </fieldset>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-12">
      <div class="">
        <div class="card-body">
          <div class="row">
            <div class="col-6">
              <div class="card">
                <div class="card-content">
                  <div class="card-body">
                    <h4 class="card-title">DETALLE DEL PRODUCTO</h4>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-6">
              <div class="card">
                <div class="card-content">
                  <div class="card-body">
                    <h4 class="card-title">DETALLE DEL SERVICIO</h4>
                  </div>
                </div>
                <div class="col-12 mb-4"></div>
                <!---->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="col-12">
      <div class="card-body">
        <div class="row">
          <div class="col-3">
            <label>SUBTOTAL:</label>
            <input
              label="precio"
              name="subtotal"
              readonly="readonly"
              placeholder="0"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-3">
            <label>DESCUENTO:</label>
            <input
              type="text"
              name="descuento"
              placeholder="0"
              aria-describedby="basic-addon2"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-3">
            <label>IVA:</label>
            <input
              type="text"
              name="iva"
              placeholder="0"
              aria-describedby="basic-addon2"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-3">
            <label>TOTAL:</label>
            <input
              label="total"
              name="total"
              readonly="readonly"
              placeholder="0"
              class="form-control form-control-sm"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="col-12 pt-4 pb-4">
      <div class="row">
        <div class="col-4">
          <button class="btn btn-success waves-effect waves-light">
            Guardar
          </button>
        </div>
        <div class="col-4">
          <select class="form-control form-control-sm col-4 offset-8">
            <option value="">Selecciona un Pago</option>
            <option value="1">EFECTIVO</option>
            <option value="2">REDBANK</option>
          </select>
        </div>
        <div class="col-4">
          <button class="btn btn-dark offset-8 waves-effect waves-light">
            Finalizar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
