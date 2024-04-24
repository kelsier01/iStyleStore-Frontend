<script setup>
	
</script>

<template>
<div id="printOTN" class="card col-10 col-md-10 col-lg-9 justify-content-center">
   <h5 class="card-header"></h5>
   <div class="card-body">
      <div class="row mt-3">
         <div class="container">
            <div class="col-12">
               <div class="row">
                  <div class="col-4">
                     <img src="/public/assets/media/istyle/logo123.png" width="250">
                     </div>
                  <div class="col-5 pr-0">
                     <h5 style="font-size: 12px;">Misael Enrique Sobrevia Rodríguez E.I.R.L.</h5>
                     <p style="font-size: 12px;">RUT: 76.325.738-K</p>
                     <p style="font-size: 12px;">Bolognesi #340 Boulevard Vereda Bolognesi Local 2</p>
                     <h5 style="font-size: 12px;">support@istylestore.cl</h5>
                     <h5 style="font-size: 12px;">www.istylestore.cl - <span><i aria-hidden="true" class="fa fa-phone-square"></i>(+569)56333621 - 58 2498666</span></h5>
                  </div>
                  <div class="col-3 numeroOT" style="text-align: center;">
                     <h3>ORDEN DE TRABAJO</h3>
                     <p class="numeroOTp">2323</p>
                  </div>
               </div>
            </div>
         </div>
      </div>
      <div class="row mt-1">
         <div class="col-9">
            <div class="card mb-3" style="background: rgb(211, 211, 211); border-radius: 10px; -webkit-print-color-adjust: exact;">
               <div class="card-body">
                  <div class="row">
                     <div id="frmIN" class="col-4">
                        <div class="form-inline">
                           <p>Nombre: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p>Contacto: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p>Equipo: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p>Codigo: </p>
                           <input type="text" class="form-control">
                        </div>
                     </div>
                     <div class="col-4">
                        <div class="form-inline">
                           <p style="width: 40px !important;">Imei: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p style="width: 40px !important;">Rut: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p>E-mail: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p>Serie: </p>
                           <input type="text" class="form-control">
                        </div>
                     </div>
                     <div class="col-4">
                        <div class="form-inline">
                           <p style="width: 113px !important; margin-left: 10px !important;">Fecha de Ingreso: </p>
                           <input type="text" class="form-control">
                        </div>
                        <div class="form-inline">
                           <p style="width: 115px !important; margin-left: 10px !important;">Fecha de Entrega: </p>
                           <input type="text" class="form-control">
                        </div>
                     </div>
                  </div>
               </div>
            </div>
         </div>
         <div class="col-3 text-center">
            <h3>TIMBRE</h3>
            <div class="rect"></div>
         </div>
      </div>
      <div class="row mt-3">
         <div class="card w-100 border-0 mb-2">
            <h3 class="card-header font-weight-bold">OBSERVACION:</h3>
            <div class="card-body">
               <div class="cajaText2">
                  <div class="row">
                     <div class="mt-3 mb-3 ml-5 col-11">
                        <p class="p-1">mantenimiento general, botón de encendido no pulsa correctamente.   2024-03-11 13:15:26</p>
                     </div>
                     <!---->
                  </div>
               </div>
            </div>
            <h3 class="card-header font-weight-bold">DIAGNÓSTICO:</h3>
            <div class="card-body">
               <div class="cajaText">
                  <div class="row">
                     <!---->
                     <div class="mt-3 mb-3 ml-5 col-11">
                        <p class="p-1">se realiza mantenimiento general, botón recupera su funcionalidad, cliente retira conforme.  2024-03-11 13:54:18</p>
                     </div>
                  </div>
               </div>
            </div>
         </div>
      </div>
      <div class="row mt-3">
         <div class="col-12">
            <table id="pagosOT" class="w-100 text-center">
               <thead>
                  <tr>
                     <th class="w-50 brtl-30">Descripción</th>
                     <th class="w-30">Precio Unitario</th>
                     <th class="w-20 brrl-30">Subtotal</th>
                  </tr>
               </thead>
               <tbody>
                  <tr>
                     <td>Cantidad:1  Mantenimiento General </td>
                     <td>29990</td>
                     <td>29990</td>
                  </tr>
               </tbody>
            </table>
         </div>
      </div>
      <div class="row mt-2">
         <div class="container">
            <div id="firmaOT" class="col-12">
               <div class="row text-center">
                  <div class="col-3">
                     <h5 class="mt-2">OT RECEPCIONADA POR</h5>
                     <h3 class="mt-1">Michael Aguirre</h3>
                     <p class="mt-6">Firma y Timbre</p>
                  </div>
                  <div class="col-3 bl-5st">
                     <h5 class="mt-2">OT RETIRADA POR</h5>
                     <div class="align-self-end">
                        <hr class="mt-7">
                        <p>FIRMA</p>
                     </div>
                  </div>
                  <div class="col-6 bl-5st">
                     <div class="w-75 m-auto">
                        <div class="form-inline mt-4">
                           <p>NETO</p>
                           <div class="tblrec form-inline w-75 d-flex justify-content-between">
                              <p>$</p>
                              <p>25202</p>
                           </div>
                        </div>
                        <div class="form-inline">
                           <p>IVA</p>
                           <div class="tblrec form-inline w-75 d-flex justify-content-between border-bottom-0 border-top-0">
                              <p>$</p>
                              <p>4788</p>
                           </div>
                        </div>
                        <div class="form-inline mb-4">
                           <p>TOTAL</p>
                           <div class="tblrec form-inline w-75 d-flex justify-content-between">
                              <p>$</p>
                              <p>29990</p>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
            </div>
         </div>
      </div>
      <div class="row">
         <div class="col-12 text-right">
            <img src="/public/assets/media/istyle/ico.png" width="100">
         </div>
      </div>
   </div>
</div>
</template>

<style>
	.cajaText{
		border: 5px solid #26e2bd;
		border-radius: 40px;
		height: auto;
	}
	.cajaText2{
		border: 5px solid #26e2bd;
		border-radius: 100px;
		height: 100px;
	}
	.tblrec{
		border: 2px solid;
		background: #d3d3d3;
		-webkit-print-color-adjust:exact;
	}
	.mt-6{
		margin-top: 4rem !important;
	}
	.mt-7{
		margin-top: 5.8rem !important;
	}
	.btnVerde{
		background-color: #26e2bd;
		border-radius: 40px !important;
		padding: 5px 20px;
		width: 60px;
	}
	hr{
		height: 10px;
		width: 50%;
		background: black;
		-webkit-print-color-adjust:exact;
		margin-bottom: 0.5rem !important;
	}
	.brtl-30{
		border-top-left-radius: 30px;
	}
	.bl-5st{
		border-left: 5px solid #26e2bd;
	}
	#pagosOT tbody tr td:nth-last-child(1){
		border-left: 5px solid #26e2bd;
	}
	#pagosOT tbody tr td:nth-last-child(3){
		border-right: 5px solid #26e2bd;
	}
	.brrl-30{
		border-top-right-radius: 30px;
	}
	#firmaOT{
		border: 5px solid #26e2bd;
		border-bottom-left-radius: 40px;
		border-bottom-right-radius: 40px;
	}
	#pagosOT{
		border-collapse: separate !important;
		border-spacing:0;
		border: 5px solid #26e2bd;
		border-top-left-radius: 40px;
		border-top-right-radius: 40px;
	}
	#pagosOT thead{
		border-collapse:collapse;
		background: #26e2bd;
		-webkit-print-color-adjust:exact;
	}
	#pagosOT th{
		color: white;
		padding-bottom: 10px !important;
		padding-top: 10px !important;
		font-weight: bold !important;
		background: none !important;
	}
	p{
		margin-bottom: 0.3rem !important;
		font-size: 1rem !important;
		
	}
	.form-inline p{
		width: 65px !important;
		margin-right: 5px !important;
		font-weight: 600 !important;
	}
	.form-inline input{
		border-radius: 20px;
		width: 159px;
		margin-bottom: 1rem !important;
	}
	h5{
		font-weight: 600 !important;
	}
	img{
		margin-top: 20px !important;
		margin-left: 10px !important;
	}
	.numeroOTp{
		font-size: 2.5rem !important;
		margin-top: 1rem !important;
		background: #26e2bd !important;
		padding: 10px 20px !important;
		color: white !important;
		border-radius: 20px !important;
		width: 200px !important;
		margin: 0 auto !important;
		-webkit-print-color-adjust:exact;
	}
	.numeroOT h3{
		margin-top: 2rem !important;
	}
	.rect{
		border: 8px solid #d3d3d3;
		width: 100%;
		height: 190px;
		border-radius: 20px;
	}
	.diag textarea{
		border: 5px solid #26e2bd;
		border-radius: 40px;
	}
	.textLo{
		border: 5px solid #26e2bd;
		border-radius: 40px;

	}
</style>
