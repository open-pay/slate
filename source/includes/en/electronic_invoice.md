# Electronic Invoice

##Generation of CFDI Object
|Field | Description|
|--------------|---------------------------|
|openpay_transaction_id|Optional <br> Id of the transaction in openpay
|invoice_id|Required<br> Invoice identifier / trade purchase order
|tipo_comprobante|Optional (default (I) income) <br> [Voucher Type Object](#voucher-type-object).
|serie|Optional (1-25 Alphanumeric) <br> series invoice in case of handling
|folio|Optional payment (1-40 Alphanumeric) <br> Folio of the invoice in case of handling
|total|Required (Decimal) <br> Total invoice
|subtotal|Required (Decimal) <br> Subtotal of the invoice
|forma_pago|Required <br> Way to pay <br> Only the payment code corresponding to the payment method must be sent. <br> [Form of Payment Object](#form-of-payment-object).
|metodo_pago|Required <br> Payment method <br> [Payment Method Object](#payment-method-object).
|lugar_expedicion|Required (5 digits) <br> Postal Code of the Place of Expedition
|descuento|Optional (Decimal) <br> Discount amount.
|observaciones|Optional (Alphanumeric) <br> Observations
|total_trasladados|Optional (Decimal) <br> Total taxes transferred if they exist
|total_retenidos|Optional (Decimal) <br> Total taxes withheld if there are
|moneda|Required (3 Alphanumeric) <br> Currency in which the sale was made in case it is different from COP. (ISO 4217)
|tipo_de_cambio|Required (Decimal) <br> Exchange rate of the currency in which the sale was made. 1.00 in case the currency is COP.
|receptor|Required ([Receiver Object](#receiver-object)) <br> Node that contains the data of the recipient of the invoice
|conceptos|Required (Arrangement of [Concept Object](#concept-object)) <br> Arrangement of concepts included in the invoice
|cfdi_relacionados|Optional ([Related Object](#related-object)) <br> Related invoices
|complements|Optional ([Complements Object](#complements-object)) <br> Complements

##Voucher Type Object
Tax receipt type  | Fiscal Document
---------      	| -----------
(I) entry 		| <li>Invoice.</li><li>Fee.</li><li>Charge note.</li><li>Donations.</li><li>Lease.</li>
(E) egress		| <li>Credit note.</li><li>Note of refund.</li><li>paysheet.</li><li>Assimilables.</li>
(T) transfer	| <li>Letter porte.</li>
(N) paysheet	| <li>paysheet.</li>
(P) Payment		| <li>Payment.</li>

##Form of Payment Object
Key  		| Description
--------- 	| -----------
01			| Cash.
02			| Cheque nominative.
03			| Electronic funds transfer.
04			| Credit card.
05			| Electronic Wallet.
06			| Electronic Money.
08			| Pantry vouchers.
12			| Dation in payment.
13			| Payment by subrogation.
14			| Payment by consignment.
15			| Condonation.
17			| Compensation.
23			| Novation.
24			| Confusion.
25			| Debt remittance.
26			| Prescription or expiration.
27			| To the satisfaction of the creditor.
28			| Debit Card.
29			| Service Card.
30			| Application of advances.
99			| Others.

##Payment Method Object
Key  		| Description
--------- 	| -----------
PUE			| Payment only exhibition
PPD			| Partial or deferred payments

##DoctoRelacionado Object
Key 			| Description         	
---------		| ---------
id_documento		|Required (16-36 Alphanumeric) <br> Document identifier (uuid).
serie				|Optional (1-25 Alphanumeric) <br> Document series.
folio				|Optional (1-40 Alphanumeric) <br> Folio of the document.
moneda_d_r			|Required (3 Alphabetical) <br> Currency Code (ISO 4217).
tipo_cambio_d_r		|Optional (Decimal) <br> Exchange rate.
metodo_de_pago_d_r	|Optional <br> Payment method.
num_parcialidad		|Optional <br> Partiality number.
imp_saldo_ant		|Optional (Decimal) <br> Amount of the previous balance.
imp_pagado			|Optional (Decimal) <br> Amount paid.
imp_saldo_insoluto	|Optional (Decimal) <br> Amount of the outstanding balance.

##Concept Object
Key 			| Description         	
---------		| ---------
Identificador	|	Required (1-100 Alphanumeric) <br> Concept identifier.
cantidad		|	Required (Decimal) <br> Amount of the concept.
unidad			|	Optional (1-20 Alphanumeric) <br> Unit of the concept.
clave_unidad	|	Required (Alphanumeric, Key Unit Catalog) <br> Unit key.
descripcion		|	Required (1-1000 Alphanumeric) <br> Description of the concept.
valor_unitario	|	Required (Decimal) <br> Unit value of the concept.
importe			|	Required (Decimal) <br> Amount of the transferred tax.
clave			|	Required (1-10 Numérico) <br> Key of the product.
descuento		|	Optional (Decimal) <br> Discount amount.
traslados		|	Optional (Arrangement [Tax Object](#tax-object)) <br> Transfer tax list.
retenciones		|	Optional (Arrangement [Tax Object](#tax-object)) <br> Retention tax list.

##Tax Object
Key 			| Description         	
---------		| ---------
impuesto		| Required <br> Tax <br> [Tax Type Object](#tax-type-object).
tipo_factor		| Required <br> Type of factor <br> <br> ***Codes:*** <br> <li>Rate</li><li>Quota</li><li>Exempt</li>
tasa			| Required <br> Decimal <br> Rate that will be used to calculate the tax
importe			| Required <br> Tax amount calculated
base			| Optional <br> Amount on which the Tax will be applied

##Tax Type Object
Code 			| Description         	
---------		| ---------
001			| ISR
002			| IVA
003			| IEPS

##Receiver Object
Field 			| Description         	
---------		| ---------
nombre				| Required (1-254 Alphanumeric) <br> Name of the recipient of the invoice.
rfc					| Required <br> RFC of the invoice recipient.
email				| Optional <br> Invoice recipient's email.
residencia_fiscal	| Optional <br> Postal code of the fiscal residence.
uso_cfdi			| Required (3 Alphanumeric) <br> [Object Use of CFDI](#use-of-cfdi-object).
pais				| Optional (3 Alphanumeric) <br> Country code (ISO 3166-1 alpha-3). It should not be sent if the RFC is registered with the SAT or is a national generic RFC.

##Use of CFDI Object
Code 			| Description         	
---------		| ---------
G01		| Acquisition of merchandise.
G02		| Returns, discounts or bonuses.
G03		| Expenses in general.
I01		| Buildings.
I02		| Office furniture and equipment for investments.
I03		| Transportation equipment.
I04		| Computer equipment and accessories.
I05		| Dices, dies, molds, matrices and tooling.
I06		| Telephone communications.
I07		| Satellite communications.
I08		| Other machinery and equipment.
D01		| Medical and dental fees and hospital expenses.
D02		| Medical expenses due to disability or disability.
D03		| Funeral expenses.
D04		| Donations.
D05		| Real interest actually paid for mortgage credits (house room).
D06		| Voluntary contributions to SAR.
D07		| Premiums for medical expenses insurance.
D08		| Mandatory school transportation expenses.
D09		| Deposits in accounts for savings, premiums based on pension plans.
D10		| Payments for educational services (tuition fees).
P01		| To define.


##Related Object
Field 			| Description         	
---------		| ---------
tipo_relacion	| Required <br> Type relationship <br> [Object Type of Relationship](#type-of-relationship-object).
relacionados	| Required (Object arrangement CfdiRelacionado) [CFDI Object Related](#cfdi-related-object).

##Type of Relationship Object
Code 			| Description         	
---------		| ---------
01	| Credit note of related documents.
02	| Debit note of related documents.
03	| Return of merchandise on previous invoices or transfers.
04	| Replacement of previous CFDIs.
05	| Goods transfers previously invoiced.
06	| Invoice generated by previous transfers.
07	| CFDI by advance payment.

##CFDI Related Object
Field 			| Description         	
---------		| ---------
uuid		|	Required (36 Alphanumeric) <br> UUID of the related invoice

##Complements Object
Field 			| Description         	
---------		| ---------
aerolineas	| Optional ([Object Complement Airlines](#complement-airlines-object)) <br> Complement for Airline.
pagos		| Optional ([Object Complement Payment](#complement-payment-object)) <br> Complement of payments.
donatarias  | Optional ([Object Complement Donee](#complement-donee-object)) <br> Complement of donee.

##Complement Airlines Object
Field 			| Description         	
---------		| ---------
tua			| Required (Decimal) <br> Airport use fee
otrosCargos	| Optional (Arrangement of [Charge Airlines Object](#charge-airlines-object)) <br> Complement of payments.

##Charge Airlines Object
Field 			| Description         	
---------		| ---------
codigo_cargo		| Optional <br> Charge code.
descripcion_cargo	| Optional <br> Charge description.
importe				| Optional (Decimal) <br> Charge amount.

##Complement Payment Object
Field 			| Description         	
---------		| ---------
fecha_pago			| Required <br> Date of the operation.
forma_de_pago		| Required <br> Way to pay.
moneda_p			| Required (Decimal) <br> Amount of the charge.
tipo_cambio_p		| Required (Decimal) <br> Exchange rate of the currency in which the sale was made. 1.00 in case the currency is COP.
monto				| Required (Decimal) <br> Payment amount.
num_operacion		| Optional (1-100 Alphanumeric) <br> Payment number.
rfc_emisor_cta_ord	| Optional <br> RFC of the issuer.
nom_banco_ord_ext	| Optional (1-300 Alphanumeric) <br> Name of the bank.
cta_ordenante		| Optional (10-50 Alphanumeric) <br> Ordering account.
rfc_emisor_cta_ben	| Beneficiary.
cta_beneficiario	| Optional (10-50 Alphanumeric) <br> Beneficiary account.
tipo_cad_pago		| Optional (único valor válido 01) <br> Type of payment chain.
cert_pago			| Optional (byte[]) <br> Payment certificate.
sello_pago			| Optional (byte[]) <br> Payment stamp.
cad_pago			| Optional (1-8192 Alphanumeric) <br> Chain.
docto_relacionados	| Optional (Arrangement [DoctoRelacionado Object](#doctorelacionado-object)).

##Complement Donee Object
Field 			| Description
---------		| ---------
no_autorizacion		| Required <br> Authorization number
fecha_autorizacion	| Required <br> Authorization date (YYYY-MM-DD)
leyenda 			| Required <br> Caption

##Request Response Generation Object
Field 			| Description         	
---------		| ---------
invoice_id		| Identifier of the invoice sent in the request.
request_id		| Request ID generated by Openpay.
date			| Date on which the generation was requested
status			| PENDING, OK, ERROR.
fiscal_status	| ACTIVE, CANCELLED.
message			| Status description.

##Notifications Object
Field 			| Description         	
---------		| ---------
invoice_id				|	Identifier of the invoice sent in the request.
serie					|	Invoice series.
folio					|	Folio of the invoice.
transaction_id			|	Openpay transaction identifier linked to the invoice.
creation_date			|	Application date.
issue_date				|	Issue date of the invoice.
uuid					|	UUID of the invoice.
receiver_rfc			|	RFC of the invoice recipient.
total					|	Total invoice.
subtotal				|	Subtotal of the invoice.
status					|	PENDING, OK, ERROR.
fiscal_status			|	ACTIVE, CANCELLED.
cancellation_date		|	Date of cancellation of the invoice in case it is canceled.
public_xml_link			|	Link to download the XML of the invoice.
public_pdf_link			|	Link to download the PDF of the invoice.
link_expiration_date	|	Expiration of the download leagues, once expired the xml / pdf can be downloaded from the dashboard.
message					|	Detail of the status of the invoice.