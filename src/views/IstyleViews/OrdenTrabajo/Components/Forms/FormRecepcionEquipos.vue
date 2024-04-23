<script setup>
  
</script>

<template>
  <div class="card-body">
        <p class="card-text"></p>
        <div class="row">
            <div class="col">
                <div class="row">
                    <div class="col-6"><label class="label-control">Run:</label></div>
                    <div class="text-right col-6" style="text-align: right;"><label class="text-right" style="text-align: right;">DNI</label> <input type="checkbox" name="run" class="text-right" style="text-align: right;" wfd-id="id2" /></div>
                </div>
                <input type="search" label="RUN" placeholder="RUN ejemplo(12345678-9)" name="run" success-text="Run Correcto" class="form-control form-control-sm" wfd-id="id3" />
            </div>
            <div class="col"><label class="label-control">IMEI:</label> <input label="IMEI" type="number" name="imei" placeholder="Imei" class="form-control form-control-sm" wfd-id="id4" /></div>
            <div class="col"><label class="label-control">Fecha Ingreso:</label> <input type="date" label="fecha Ingreso" id="fechaActual" name="fecha" placeholder="fecha" class="form-control form-control-sm" wfd-id="id5" /></div>
        </div>
        <div class="row">
            <div class="col">
                <label class="label-control">Contacto:</label>
                <div class="input-group">
                    <div class="input-group-prepend"><div class="input-group-text">+569</div></div>
                    <input type="number" size="8" maxlength="8" oninput="if(this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" placeholder="Contacto" name="fono" id="fono" class="form-control form-control-sm" wfd-id="id6" />
                </div>
            </div>
            <div class="col"><label class="label-control">Nombre:</label> <input label="nombre" name="nombre" placeholder="nombre" id="nombre" class="form-control form-control-sm" wfd-id="id7" /></div>
            <div class="col"><label class="label-control">Fecha Entrega:</label> <input type="date" label="fecha Entrega" placeholder="fecha entrega" name="fechaentrega" class="form-control form-control-sm" wfd-id="id8" /></div>
        </div>
        <div class="row">
            <div class="col">
                <label class="label-control">Equipo:</label>
                <select class="form-control form-control-sm">
                    <option value="1">iPhone</option>
                    <option value="2">Macbook</option>
                    <option value="3">iPad</option>
                    <option value="12">Magsafe 2</option>
                    <option value="13">MagSafe 1</option>
                    <option value="14">MagSafe 1</option>
                    <option value="15">iMac</option>
                </select>
            </div>
            <div class="col">
                <label class="label-control">Modelo:</label> <input type="hidden" name="" wfd-id="id9" />
                <select class="form-control form-control-sm">
                    <option value="2">iPhone 5</option>
                    <option value="3">iPhone 5c</option>
                    <option value="4">iPhone 5s</option>
                    <option value="5">iPhone SE</option>
                    <option value="6">iPhone 6</option>>
                </select>
            </div>
            <div class="col"><label class="label-control">Mail:</label> <input type="mail" label="Mail" id="mail" name="mail" placeholder="Mail" success-text="Run Correcto" class="form-control form-control-sm" wfd-id="id10" /></div>
        </div>
        <div class="row">
            <div class="col"><label class="label-control">Codigo:</label> <input label="codigo" placeholder="codigo" name="codigo" class="form-control form-control-sm" wfd-id="id11" /></div>
            <div class="col"><label class="label-control">Serie:</label> <input label="RUN" placeholder="serie" name="serie" success-text="Run Correcto" class="form-control form-control-sm" wfd-id="id12" /></div>
            <div class="col">
                <input type="hidden" name="id_cliente" id="id_cliente" wfd-id="id13" /> <label class="label-control">Valor Diagnostico:</label>
                <div class="input-group">
                    <div class="input-group-prepend"><div class="input-group-text">$</div></div>
                    <input type="number" label="RUN" placeholder="0" name="serie" success-text="Run Correcto" class="form-control form-control-sm" wfd-id="id14" />
                </div>
            </div>
        </div>
    </div>
</template>

<style>
  
</style>