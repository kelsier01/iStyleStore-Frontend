<script setup>
	
</script>

<template>
	<div class="container">
   <div class="row">
      <div class="col-md-12">
         <div class="text-right"><button type="button" class="btn btn-primary mb-3 waves-effect waves-light">Imprimir Orden de Trabajo</button></div>
         <div id="printOTN" class="card card col-10 col-md-10 col-lg-12 justify-content-center">
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
                              <h3 style="font-size: 12px;">RUT: 76.325.738-K</h3>
                              <h4 style="font-size: 12px;">Bolognesi #340 Boulevard Vereda Bolognesi Local 2 y 18</h4>
                              <h5 style="font-size: 12px;"><i class="fa fa-at"></i> support@istylestore.cl - <i class="fa fa-globe"></i> www.istylestore.cl
                              </h5>
                              <h5 style="font-size: 12px;"><i aria-hidden="true" class="fa fa-phone-square"></i> +56 9 56333621 -  <i aria-hidden="true" class="fa fa-phone-square"></i> 58 2 498666</h5>
                           </div>
                           <div class="col-3 text-center">
                              <h3>ORDEN DE TRABAJO</h3>
                              <p class="numeroOTp">2323</p>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div class="row mt-4">
                  <div class="col-12">
                     <div class="card mb-3" style="background-color: rgb(211, 211, 211); border-radius: 10px; -webkit-print-color-adjust: exact;">
                        <div class="card-body">
                           <div class="row">
                              <div class="col-3">
                                 <div class="form-inline">
                                    <p>Nombre: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                                 <div class="form-inline">
                                    <p>Equipo: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                              </div>
                              <div class="col-3">
                                 <div class="form-inline">
                                    <p style="width: 40px !important;">Rut: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                                 <div class="form-inline">
                                    <p style="width: 40px !important;">Imei: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                              </div>
                              <div class="col-3">
                                 <div class="form-inline">
                                    <p>Telefono: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                                 <div class="form-inline">
                                    <p>Codigo: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                              </div>
                              <div class="col-3">
                                 <div class="form-inline">
                                    <p>E-mail: </p>
                                    <input type="text" class="form-control form-control-sm">
                                 </div>
                                 <div class="form-inline">
                                    <p>Serie: </p>
                                    <input type="text" class="form-control form-control-sm">
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
                                 <div class="col-9"><b style="font-size: 14px;">¿el equipo se encuentra encendido?</b></div>
                                 <div class="col-3 mt-1 text-center">
                                    <div v="" class="btnVerde" style="font-size: 12px;">SI</div>
                                    <div class="btnRojo" style="font-size: 12px; display: none;">No</div>
                                 </div>
                              </div>
                           </div>
                        </div>
                     </div>
                     <div class="col-12 mt-1">
                        <div class="row">
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Equipo presenta imagen? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona botón de volumen y silencio? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona el FLASH y VIBRADOR? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona el puerto de carga y jack de audio? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona Auricular y Bocina de Altavoces? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Equipo ha sido manipulado anteriormente? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona sensor de proximidad? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Contacto con alguna especia de líquido, de forma directa o indirecta? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white;">poca</b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona cámara frontal y trasera? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Usa cargador original? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona Face ID? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona botón HOME, TOUCH ID? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona WI-FI? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona botón POWER? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Funciona el táctil en su totalidad? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>PORCENTAJE DE BATERÍA </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white;">95</b></label></div>
                                 <div class="col-3 text-center">
                                    <div class="btnVerde" style="-webkit-print-color-adjust: exact; font-size: 12px;"> Si
                                    </div>
                                    <!---->
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>Equipo presenta abollones, golpes, caídas y eventos que dañen el cuerpo del equipo? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <!----> 
                                    <div class="btnRojo" style="-webkit-print-color-adjust: exact; font-size: 12px;"> No
                                    </div>
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>Presenta en la pantalla ¿Golpes, roturas, trizaduras? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <!----> 
                                    <div class="btnRojo" style="-webkit-print-color-adjust: exact; font-size: 12px;"> No
                                    </div>
                                 </div>
                              </div>
                           </div>
                           <div class="col-6 mt-2">
                              <div class="row">
                                 <div class="col-9"><label style="font-size: 14px;"><b>¿Falta algún perno de seguridad? </b> <b style="font-size: 14px; background-color: rgb(37, 48, 63); border-radius: 4px; padding: 2px 5px; color: white; display: none;"></b></label></div>
                                 <div class="col-3 text-center">
                                    <!----> 
                                    <div class="btnRojo" style="-webkit-print-color-adjust: exact; font-size: 12px;"> No
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
                           <div class="col-6" style="border-right: 5px solid rgb(38, 226, 189);"><textarea rows="3" class="border-0 w-100 pl-2 pt-1 mt-2"></textarea></div>
                           <div class="col-3 text-center" style="align-self: flex-end;">
                              <p>Firma</p>
                           </div>
                           <div class="col-3" style="border-left: 5px solid rgb(38, 226, 189); display: flex; justify-content: center; align-items: center;">
                              <h2>$ 29990</h2>
                           </div>
                        </div>
                     </div>
                     <div class="card-body ">
                        <div class="row ml-2">
                           <div class="col-4">
                              <div style="font-size: 14px;">Nombre del Tecnico: Michael Aguirre</div>
                           </div>
                           <div class="col-4">
                              <div style="font-size: 14px;">Fecha de Ingreso: 2024-03-11 13:15:26</div>
                           </div>
                           <div class="col-4">
                              <div style="font-size: 14px;">Fecha de Entrega: 2024-03-11 13:15:26</div>
                           </div>
                        </div>
                     </div>
                  </div>
                  <div class="col-12 text-right">
                     <img src="/public/assets/media/istyle/ico.png" width="100">
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
</div>
</template>

<style>

	@media print {
		header {display:none;}
		footer {display:none;}
	}
	.tblrec{
		border: 2px solid;
		background-color: #d3d3d3;
	}
	.mt-6{
		margin-top: 4rem !important;
	}
	.mt-7{
		margin-top: 5.8rem !important;
	}
	hr{
		height: 10px;
		width: 50%;
		background-color: black;
		margin-bottom: 0.5rem !important;
	}
	.btnVerde{
		background-color: #26e2bd;
		border-radius: 40px !important;
		padding: 5px 15px;
		width: 55px;
	}
	.btnRojo{
		background-color: rgb(238, 75, 75);
		color:#000;
		border-radius: 40px !important;
		padding: 10px 13px;
		width: 55px;
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
		background-color: #26e2bd;
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
		margin-right: 5px;
		font-weight: 600 ;
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
	.areatext{
		border: 5px solid #26e2bd;
		border-radius: 40px;	
	}

	.areatext2{
		border: 5px solid #26e2bd;
		border-radius: 0px 0px 40px 40px;	

	}
	.areatext3{
		border: 5px solid #26e2bd;
		border-radius: 0px 0px 0px 0px;	

	}

</style>
