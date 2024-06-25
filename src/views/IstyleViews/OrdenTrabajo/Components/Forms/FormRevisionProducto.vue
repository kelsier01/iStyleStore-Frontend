<script setup></script>

<template>
  <div class="row">
    <div class="col-12">
      <div class="card-body">
        <div class="row">
          <div class="col-md-3">
            <label>SUBTOTAL:</label>
            <input
              label="precio"
              name="subtotal"
              readonly="readonly"
              placeholder="0"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-md-3">
            <label>DESCUENTO:</label>
            <input
              type="text"
              name="descuento"
              placeholder="0"
              aria-describedby="basic-addon2"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-md-3">
            <label>IVA:</label>
            <input
              type="text"
              name="iva"
              placeholder="0"
              aria-describedby="basic-addon2"
              class="form-control form-control-sm"
            />
          </div>
          <div class="col-md-3">
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
  </div>
</template>

<style></style>
