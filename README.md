# Lab 16 - Aislamiento de Storage con Private Endpoint (Private Link)

## Objetivo
Configurar un Storage Account en Azure para que **no sea accesible desde Internet público** y que todo el acceso a los datos se realice **exclusivamente a través de la red privada**, utilizando Private Endpoint y resolución DNS privada.

El objetivo es simular un escenario real donde los datos sensibles no deben exponerse públicamente.

---

## Qué he hecho en este laboratorio

1. He creado un Storage Account para pruebas.
2. He desplegado un Private Endpoint (Private Link) para el servicio Blob dentro de la subnet BackEnd.
3. He deshabilitado completamente el acceso por red pública al Storage Account.
4. He configurado (o validado) la resolución DNS privada para que, desde la VNet, el nombre del Storage resuelva a una IP privada.
5. He validado que el acceso al Storage se realiza por red privada y no por Internet.

---

## Arquitectura y concepto
El Storage Account mantiene su nombre público (`*.blob.core.windows.net`), pero gracias a Private Endpoint:

- El tráfico no sale a Internet.
- El nombre público se resuelve internamente a una IP privada (`10.x.x.x`).
- El acceso público queda bloqueado a nivel de red.

Este enfoque reduce la superficie de ataque y es habitual en entornos empresariales.

---

## Configuración utilizada

- VNet: `VNET-LAB12`
- Subnet: `snet-backend`
- Storage Account: `stlab16antonio`
- Servicio protegido: Blob
- Private Endpoint:
  - Nombre: `pe-stlab16-blob`
  - Subrecurso: `blob`
  - IP privada asignada en `snet-backend`
- Acceso público: deshabilitado
- DNS privado:
  - Zona: `privatelink.blob.core.windows.net`
  - Vinculada a la VNet

---

## Validación funcional (prueba real)

### Resolución DNS desde dentro de la red
Desde una máquina virtual situada en `snet-backend`, he ejecutado:

```bash
nslookup stlab16antonio.blob.core.windows.net
