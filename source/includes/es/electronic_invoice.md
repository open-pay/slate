# Facturación Electronica

##Objeto Generación de CFDI
|Campo 	|Descripción         	|
|--------------|---------------------------|
|openpay_transaction_id|Opcional<br> Id de la transacción en openpay.
|invoice_id|Requerido<br> Identificador de factura /orden de compra del comercio.
|tipo_comprobante|Opcional (default (I) ingreso) <br> [Objeto Tipo de Comprobante](#objeto-tipo-de-comprobante).
|serie|Opcional (1-25 Alfanumérico) <br> Serie de la factura en caso de manejar.
|folio|Opcional pago (1-40 Alfanumérico) <br> Folio de la factura en caso de manejar.
|total|Requerido (Decimal) <br> Total de la factura.
|subtotal|Requerido (Decimal) <br> Subtotal de la factura.
|forma_pago|Requerido <br> Forma de pago <br> Se debe enviar solamente la clave de pago que corresponda al método de pago realizado. <br> [Objeto Forma de Pago](#objeto-forma-de-pago).
|metodo_pago|Requerido <br> Método de pago <br> [Objeto Metodo de Pago](#objeto-metodo-de-pago).
|lugar_expedicion|Requerido (5 dígitos) <br> Código postal del Lugar de expedición.
|descuento|Opcional (Decimal) <br> Monto del descuento.
|observaciones|Opcional (Alfanumérico) <br> Observaciones.
|total_trasladados|Opcional (Decimal) <br> Total de impuestos trasladados en caso que existan.
|total_retenidos|Opcional (Decimal) <br> Total de impuestos retenidos en caso que existan.
|moneda|Requerido (3 Alfanumerico) <br> Moneda en la que se realizó la venta en caso que sea diferente de COP. (ISO 4217)
|tipo_de_cambio|Requerido (Decimal) <br> Tipo de cambio de la moneda en la que se realizó la venta. 1.00 en caso que la moneda sea COP.
|receptor|Requerido ([Objeto Receptor](#objeto-receptor)) <br> Nodo que contiene los datos del receptor de la factura.
|conceptos|Requerido (Arreglo de [Objeto Concepto](#objeto-concepto)) <br> Arreglo de conceptos incluidos en la factura.
|cfdi_relacionados|Opcional ([Objeto Relacionados](#objeto-relacionado)) <br> Facturas relacionadas.
|complements|Opcional ([Objeto Complementos](#objeto-complementos)) <br> Complementos.

##Objeto Tipo de Comprobante
Tipo comprobante fiscal  | Documento Fiscal
---------      	| -----------
(I) ingreso		|<li>Factura.</li><li>Honorarios.</li><li>Nota de cargo.</li><li>Donativos.</li><li>Arrendamiento.</li>
(E) egreso		|<li>Nota de crédito.</li><li>Nota de devolución.</li><li>Nómina.</li><li>Asimilables.</li>
(T) traslado	|<li>Carta porte.</li>
(N) Nómina		|<li>Nómina.</li>
(P) Pago		|<li>Pago.</li>

##Objeto Forma de Pago
Clave  		| Descripción
--------- 	| -----------
01			| Efectivo.
02			| Cheque nominativo.
03			| Transferencia electrónica de fondos.
04			| Tarjeta de Crédito.
05			| Monedero Electrónico.
06			| Dinero Electrónico.
08			| Vales de despensa.
12			| Dación en pago.
13			| Pago por subrogación.
14			| Pago por consignación.
15			| Condonación.
17			| Compensación.
23			| Novación.
24			| Confusión.
25			| Remisión de deuda.
26			| Prescripción o caducidad.
27			| A satisfacción del acreedor.
28			| Tarjeta de Débito.
29			| Tarjeta de Servicio.
30			| Aplicación de anticipos.
99			| Otros.

##Objeto Metodo de Pago
Clave  		| Descripción
--------- 	| -----------
PUE			| Pago única exhibición.
PPD			| Pagos parciales o diferidos.

##Objeto DoctoRelacionado
Clave 			| Descripción         	
---------		| ---------
id_documento		| Requerido (16-36 Alfanumérico) <br> Identificador del documento (uuid).
serie				| Opcional (1-25 Alfanumérico) <br> Serie del documento.
folio				| Opcional (1-40 Alfanumérico) <br> Folio del documento.
moneda_d_r			| Requerido (3 Alfabético) <br> Código de Moneda (ISO 4217).
tipo_cambio_d_r		| Opcional (Decimal) <br> Tipo de cambio.
metodo_de_pago_d_r	| Opcional <br> Método de pago.
num_parcialidad		| Opcional <br> Número de la parcialidad.
imp_saldo_ant		| Opcional (Decimal) <br> Importe del saldo anterior.
imp_pagado			| Opcional (Decimal) <br> Importe pagado.
imp_saldo_insoluto	| Opcional (Decimal) <br> Importe del saldo insoluto.


##Objeto Concepto
Clave 			| Descripción         	
---------		| ---------
Identificador	| Requerido (1-100 Alfanumérico) <br> Identificador del concepto.
cantidad		| Requerido (Decimal) <br> Cantidad del concepto.
unidad			| Opcional(1-20 Alfanumérico) <br> Unidad del concepto.
clave_unidad	| Requerido (Alfanumérico, Catálogo Clave Unidad) <br> Clave de unidad.
descripcion		| Requerido (1-1000 Alfanumérico) <br> Descripción del concepto.
valor_unitario	| Requerido (Decimal) <br> Valor unitario del concepto.
importe			| Requerido (Decimal) <br> Importe del impuesto trasladado.
clave			| Requerido (1-10 Numérico) <br> Clave del producto.
descuento		| Opcional (Decimal) <br> Monto de descuento.
traslados		| Opcional (Arreglo de [Objeto Impuesto](#objeto-impuesto)) <br> Lista de impuestos de traslado.
retenciones		| Opcional (Arreglo de [Objeto Impuesto](#objeto-impuesto)) <br> Lista de impuestos de retención.

##Objeto Impuesto
Clave 			| Descripción         	
---------		| ---------
impuesto		| Requerido <br> Impuesto <br> [Objeto Tipo de Impuesto](#objeto-tipo-de-impuesto).
tipo_factor		| Requerido <br> Tipo de factor <br> ***Códigos:*** <br> <li>Tasa</li><li>Cuota</li><li>Excento</li>
tasa			| Requerido <br> Decimal <br> Tasa que será usada para calcular el impuesto
importe			| Requerido <br> Monto del impuesto calculado
base			| Opcional <br> Monto sobre el cual será aplicado el Impuesto

##Objeto Tipo de Impuesto
Código 		| Descripción         	
---------	| ---------
001			| ISR
002			| IVA
003			| IEPS

##Objeto Receptor
Campo 			| Descripción         	
---------		| ---------
nombre				| Requerido (1-254 Alfanumérico) <br> Nombre del receptor de la factura.
rfc					| Requerido <br> RFC del receptor de la factura.
email				| Opcional <br> Email del receptor de la factura.
residencia_fiscal	| Opcional <br> Código postal de la residencia fiscal.
uso_cfdi			| Requerido (3 Alfanumérico) <br> [Objeto Uso de CFDI](#objeto-uso-de-cfdi).
pais				| Opcional (3 Alfanumérico) <br> Código de país (ISO 3166-1 alfa-3). No debe enviarse si el RFC está registrado con el SAT o es un RFC genérico nacional.

##Objeto Uso de CFDI
Código 		| Descripción         	
---------	| ---------
G01		| Adquisición de mercancías.
G02		| Devoluciones, descuentos o bonificaciones.
G03		| Gastos en general.
I01		| Construcciones.
I02		| Mobiliario y equipo de oficina por inversiones.
I03		| Equipo de transporte.
I04		| Equipo de computo y accesorios.
I05		| Dados, troqueles, moldes, matrices y herramental.
I06		| Comunicaciones telefónicas.
I07		| Comunicaciones satelitales.
I08		| Otra maquinaria y equipo.
D01		| Honorarios médicos, dentales y gastos hospitalarios.
D02		| Gastos médicos por incapacidad o discapacidad.
D03		| Gastos funerarios.
D04		| Donativos.
D05		| Intereses reales efectivamente pagados por créditos hipotecarios (casa habitación).
D06		| Aportaciones voluntarias al SAR.
D07		| Primas por seguros de gastos médicos.
D08		| Gastos de transportación escolar obligatoria.
D09		| Depósitos en cuentas para el ahorro, primas que tengan como base planes de pensiones.
D10		| Pagos por servicios educativos (colegiaturas).
P01		| Por definir.


##Objeto Relacionado
Campo 			| Descripción         	
---------		| ---------
tipo_relacion	| Requerido <br> Tipo relación <br> [Objeto Tipo de Relación](#objeto-tipo-de-relaci-n).
relacionados	| Requerido (Arreglo de Objeto CfdiRelacionado) <br> [Objeto CFDI Relacionado](#objeto-cfdi-relacionado).

##Objeto Tipo de Relación
Código 			| Descripción         	
---------		| ---------
01	| Nota de crédito de los documentos relacionados.
02	| Nota de débito de los documentos relacionados.
03	| Devolución de mercancía sobre facturas o traslados previos.
04	| Sustitución de los CFDI previos.
05	| Traslados de mercancías facturados previamente.
06	| Factura generada por los traslados previos.
07	| CFDI por aplicación de anticipo.

##Objeto CFDI Relacionado
Campo 			| Descripción         	
---------		| ---------
uuid		|	Requerido (36 Alfanumérico) <br> UUID de la factura relacionada.

##Objeto Complementos
Campo 			| Descripción         	
---------		| ---------
aerolineas	| Opcional ([Objeto Complemento Aerolíneas](#objeto-complemento-aerol-neas)) <br> Complemento para aerolíneas.
pagos		| Opcional ([Objeto Complemento Pago](#objeto-complemento-pago)) <br> Complementos de pago.
donatarias  | Opcional ([Objeto Complemento Donatarias](#objeto-complemento-donatarias)) <br> Complemento Donatarias.


##Objeto Complemento Aerolíneas
Campo 			| Descripción         	
---------		| ---------
tua			| Requerido (Decimal) <br> Tarifa de uso de aeropuerto.
otrosCargos	| Opcional (Arreglo de [Objeto Aerolíneas Cargo](#objeto-aerol-neas-cargo)) <br> Complementos de pago.


##Objeto Aerolíneas Cargo
Campo 			| Descripción         	
---------		| ---------
codigo_cargo		| Opcional <br> Código del cargo.
descripcion_cargo	| Opcional <br> Descripción del cargo.
importe				| Opcional (Decimal) <br> Monto del cargo.


##Objeto Complemento Pago
Campo 			| Descripción         	
---------		| ---------
fecha_pago			| Requerido <br> Fecha de la operación.
forma_de_pago		| Requerido <br> Forma de pago.
moneda_p			| Requerido (Decimal) <br> Monto del cargo.
tipo_cambio_p		| Requerido (Decimal) <br> Tipo de cambio de la moneda en la que se realizó la venta. 1.00 en caso que la moneda sea COP.
monto				| Requerido (Decimal) <br> Monto del pago.
num_operacion		| Opcional (1-100 Alfanumérico) <br> Número de pago.
rfc_emisor_cta_ord	| Opcional <br> RFC del emisor.
nom_banco_ord_ext	| Opcional (1-300 Alfanumérico) <br> Nombre del banco.
cta_ordenante		| Opcional (10-50 Alfanumérico) <br> Cuenta ordenante.
rfc_emisor_cta_ben	| Beneficiario.
cta_beneficiario	| Opcional (10-50 Alfanumérico) <br> Cuenta del beneficiario.
tipo_cad_pago		| Opcional (único valor válido 01) <br> Tipo de cadena de pago.
cert_pago			| Opcional (byte[]) <br> Certificado de pago.
sello_pago			| Opcional (byte[]) <br> Sello de pago.
cad_pago			| Opcional (1-8192 Alfanumérico) <br> Cadena.
docto_relacionados	| Opcional (Arreglo [Objeto DoctoRelacionado](#objeto-doctorelacionado)).

##Objeto Complemento Donatarias
Campo 			| Descripción         	
---------		| ---------
no_autorizacion		| Requerido <br> Número de autorización
fecha_autorizacion	| Requerido <br> Fecha de autorización (YYYY-MM-DD)
leyenda 			| Requerido <br> Leyenda

##Objeto Respuesta de solicitud de generación
Campo 			| Descripción         	
---------		| ---------
invoice_id		| Identificador de la factura enviado en la solicitud.
request_id		| Id de petición generado por Openpay.
date			| Fecha en que se solicito la generación.
status			| PENDING, OK, ERROR.
fiscal_status	| ACTIVE, CANCELLED.
message			| Description del status.

##Objeto Notificaciones
Campo 			| Descripción         	
---------		| ---------
invoice_id				|	Identificador de la factura enviado en la solicitud.
serie					|	Serie de la factura.
folio					|	Folio de la factura.
transaction_id			|	Identificador de transacción de Openpay ligado a la factura.
creation_date			|	Fecha de solicitud.
issue_date				|	Fecha de emisión de la factura.
uuid					|	UUID de la factura.
receiver_rfc			|	RFC del receptor de la factura.
total					|	Total de la factura.
subtotal				|	Subtotal de la factura.
status					|	PENDING, OK, ERROR.
fiscal_status			|	ACTIVE, CANCELLED.
cancellation_date		|	Fecha de cancelación de la factura en caso que este cancelada.
public_xml_link			|	Liga para descarga del xml de la factura.
public_pdf_link			|	Liga para descarga del pdf de la factura.
link_expiration_date	|	Expiración de las ligas de descarga, una vez expiradas los xml / pdf pueden ser escargados desde el dashboard.
message					|	Detalle del status de la factura.































