<script setup>
    
</script>

<template>
    <div class="card-body">
        <div class="col-12"><label>Observacion:</label> <textarea disabled="disabled" name="falla" rows="4" class="form-control mt-2 mb-5 large-textarea"></textarea></div>
        <div class="col-12"><label>Diagnostico:</label> <textarea name="diagnostico" rows="4" class="form-control mt-2 mb-5 large-textarea"></textarea></div>
            <div class="col-12">
                <div class="row">
                    <div class="col-6">
                        <div class="row">
                            <div class="col-2"><label>Estados:</label></div>
                            <div class="col-4">
                                <select class="form-control">
                                    <option value="diagnostico">En diagnostico</option>
                                    <option value="Reparacion">En proceso de Reparacion</option>
                                    <option value="Pruebas">En proceso de Pruebas</option>
                                    <option value="Retirar">Listo para Retirar</option>
                                    <option vlaue="bodega">En Bodega</option>
                                    <option value="entregado">Entregado</option>
                                </select>
                            </div>
                        </div>
                    </div>
                    <div class="col-6"><div class="offset-8"></div></div>
                </div>
            </div>
    </div>

</template>

<style>
    
</style>