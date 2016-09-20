# Tax-Help
Aplicación de primer proyecto en TICs


def calculoImpuestoAPagar(honorarios, sueldos):
	UTA = 551988 			#Unidad tributaria anual
	GP = honorarios * 0.3 	#Gastos presuntos
	if honorarios > 15 * UTA:
		honorarios = 15 * UTA
	if sueldos < 7282710:
		FG = 0 	#Factor tabla impuesto global
		CAR = 0 #Cantidad a rebajar tabla impuesto global
	if sueldos >= 7282710 and sueldos <= 16183800:
		FG = 0.04 
		CAR = 291308
	if sueldos >= 16183801 and sueldos <= 26973000:
		FG = 0.08 
		CAR = 938660
	if sueldos >= 26973001 and sueldos <= 37762200:
		FG = 0.135
		CAR = 2422175
	if sueldos >= 37762201 and sueldos <= 48551400:
		FG = 0.23
		CAR = 6009584
	if sueldos >= 48551401 and sueldos <= 64735200:
		FG = 0.304
		CAR = 9602388
	if sueldos >= 64735201 and sueldos <= 80919000:
		FG = 0.335
		CAR = 12903883
	if sueldos >= 80919001:
		FG = 0.4
		CAR = 16545238

	IAP = ((honorarios - GP + sueldos) * FG) - CAR #Impuesto a pagar
	return IAP

def calculoImpuestoRetenido(sueldo):
	IR=0 #Impuesto retenido
	for i in range(0,11):
		if sueldo[i] < 620986:
			F2 = 0 	#Factor impuesto unico segunda categoria
			CAR2 = 0  #Cantidad a rebajar segunda categoria
		if sueldo[i] >= 620986 and sueldo[i] <= 1379970:
			F2 = 0.04
			CAR2 = 24839
		if sueldo[i] >= 1379971 and sueldo[i] <= 2299950:
			F2 = 0.08
			CAR2 = 80038
		if sueldo[i] >= 2299951 and sueldo[i] <= 3219930:
			F2 = 0.135
			CAR2 = 206535
		if sueldo[i] >= 3219931 and sueldo[i] <= 4139910:
			F2 = 0.23
			CAR2 = 512428
		if sueldo[i] >= 4139911 and sueldo[i] <= 5519880:
			F2 = 0.304
			CAR2 = 818782
		if sueldo[i] >= 5519881 and sueldo[i] <= 6899850:
			F2 = 0.355
			CAR2 = 1100296
		if sueldo[i] >= 6899851:
			F2 = 0.4
			CAR2 = 1410789
		IR = IR + ((sueldo[i] * F2) - CAR2)
	return IR

sueldo = [0]*12 #Ingresar cada sueldo en la lista [0-11]
honorarios = 0  #Ingresar honorarios

sueldos = 0 	#Sumatoria de los sueldos
for k in sueldo:
	sueldos = sueldos + k

impuestoPorPagar = calculoImpuestoAPagar(honorarios,sueldos)
impuestoRetenido = calculoImpuestoRetenido(sueldo)

impuestoTotal = impuestoPorPagar - impuestoRetenido
if impuestoTotal < 0:
	print'Su devolucion de impuestos corresponde a: ', impuestoTotal
if impuestoTotal >= 0:
	print'Usted debe pagar: ', impuestoTotal
