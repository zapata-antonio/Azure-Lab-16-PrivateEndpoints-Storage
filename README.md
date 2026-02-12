# Lab 16 - Storage aislado con Private Endpoint (Private Link)

## Objetivo
Configurar un Storage Account para que el acceso a los datos no salga por Internet público. La idea es que el almacenamiento solo sea accesible desde la red privada de Azure mediante Private Link.

## Qué he hecho en este laboratorio
1. He creado un Storage Account para pruebas.
2. He desplegado un Private Endpoint para el servicio Blob dentro de la subnet BackEnd.
3. He deshabilitado el acceso por red pública al Storage.
4. (Opcional) He dejado configurada la resolución DNS privada para que, desde dentro de la VNet, el nombre del Storage resuelva a la IP privada del Private Endpoint.

## Configuración utilizada
- VNet: `VNET-LAB12`
- Subnet: `snet-backend`
- Storage Account: (tu nombre real aquí)
- Private Endpoint: asociado a `blob` y con IP privada en BackEnd
- (Opcional) Private DNS Zone: `privatelink.blob.core.windows.net` vinculada a la VNet

## Evidencias

### 01 - Private Endpoint aprobado y con IP privada
[<img src="images/01-private-endpoint.png" width="800">](images/01-private-endpoint.png)

### 02 - Acceso público deshabilitado
[<img src="images/02-public-disabled.png" width="800">](images/02-public-disabled.png)

## Checklist de verificación
- [ ] Public network access deshabilitado en el Storage Account
- [ ] Private Endpoint en estado Approved/Connected y con IP privada asignada

## Qué le diría a un cliente o en entrevista
“Con Private Endpoints el Storage deja de estar expuesto a Internet. El tráfico entra por la red privada de Azure y, si además configuras DNS privado, los servicios resuelven el Storage a una IP interna sin necesidad de rutas raras ni aperturas de red.”
