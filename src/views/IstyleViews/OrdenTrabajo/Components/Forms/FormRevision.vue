<script setup>
    
</script>

<template>
        <div class="card-body">
            <div class="row">
                <div class="col-4">
                    <input type="search" name="" class="form-control form-control-sm " />
                    <div class="list-group country-list3" style="position: absolute;"></div>
                </div>
                <div class="col-6"><button class="btn btn-dark waves-effect waves-light">Buscar</button></div>
                <div class="col-2">
                    ORDEN Nº
                </div>
            </div>
            <br />
            <input type="hidden" name="" />
            <div class="algo">
                <div class="row">
                    <div class="col"><label>Run:</label> <input type="search" label="RUN" placeholder="RUN" name="run" success-text="Run Correcto" class="form-control form-control-sm " /></div>
                    <div class="col"><label>IMEI:</label> <input label="IMEI" name="imei" placeholder="Imei" readonly="readonly" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Fecha Ingreso:</label> <input type="text" label="fecha Ingreso" id="fechaActual" name="fecha" placeholder="fecha" readonly="readonly" class="form-control form-control-sm " /></div>
                </div>
                <div class="row">
                    <div class="col"><label>Contacto:</label> <input placeholder="Contacto" name="fono" id="fono" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Nombre:</label> <input label="nombre" name="nombre" placeholder="nombre" id="nombre" onkeyup="javascript:this.value=this.value.toUpperCase();" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Fecha Entrega:</label> <input type="datetime-local" label="fecha Entrega" placeholder="fecha entrega" name="fechaentrega" class="form-control form-control-sm " /></div>
                </div>
                <div class="row">
                    <div class="col"><label>Equipo:</label> <input type="text" name="" readonly="readonly" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Modelo:</label> <input type="text" name="" readonly="readonly" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Mail:</label> <input type="mail" label="Mail" id="mail" name="mail" placeholder="Mail" success-text="Run Correcto" class="form-control form-control-sm " /></div>
                </div>
                <div class="row">
                    <div class="col"><label>Codigo:</label> <input label="codigo" placeholder="codigo" name="codigo" readonly="readonly" class="form-control form-control-sm " /></div>
                    <div class="col"><label>Serie:</label> <input label="RUN" placeholder="serie" name="serie" success-text="Run Correcto" readonly="readonly" class="form-control form-control-sm " /></div>
                    <div class="col"><input type="hidden" name="id_cliente" id="id_cliente" /> <input type="hidden" name="id_ordenes" id="id_ordenes" /></div>
                </div>
            </div>
        </div>
</template>

<style>
    
</style>