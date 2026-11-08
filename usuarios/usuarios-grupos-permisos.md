# Usuarios, grupos y permisos

La idea es sencilla: **cada persona solo puede hacer lo que necesita para su trabajo**, y nada más. Así se evitan errores y se protege la información.

Por seguridad, aquí no hay contraseñas. Solo el correo con el que entra cada persona.

## Quién es quién

| Persona | Correo | Puesto | Tipo | Qué puede hacer | Por qué |
|---|---|---|---|---|---|
| Lucía Fernández | lucia@lupuloerrante.example | Comercial | Interno | Ventas: solo ve y gestiona lo suyo. Facturación e Inventario: no tiene. Grupo propio: Lúpulo Errante / Comercial junior | Solo prepara presupuestos para sus clientes. No necesita la parte de dinero |
| Carlos Mendoza | carlos@lupuloerrante.example | Responsable de ventas | Interno | Ventas: puede hacerlo todo. Inventario: puede usarlo. Facturación: no tiene | Ve todos los presupuestos, los confirma y da la salida a los pedidos |
| Ignacio Sedano | ignacio@lupuloerrante.example | Administración y facturas | Interno | Facturación: puede crear facturas y cobrar. Ventas: puede ver todos los pedidos, pero no es jefe de Ventas. Inventario: no tiene | Necesita ver el pedido para hacer la factura. No toca el almacén |
| Marta Ruiz Salgado | marta.ruiz@cliente.example | Cliente | Portal | Solo ve sus propios presupuestos y facturas | Es una persona de fuera de la empresa |

## Los tres tipos de usuario

- **Interno:** persona que trabaja en la empresa. Entra en Odoo con los permisos que se le dan (Lucía, Carlos e Ignacio).
- **Portal:** cliente que entra a una zona especial donde solo ve sus propios documentos (Marta).
- **Público:** persona que visita la web sin entrar con usuario. No puede ver nada privado.

## Grupo propio: Lúpulo Errante / Comercial junior

Un grupo es un conjunto de permisos que se le da a una persona de una vez.

- **Lo tiene:** Lucía Fernández.
- **Parte de los permisos de:** Ventas, solo documentos propios. Es decir, ya incluye todo lo de ese grupo y le añadimos más cosas.

En la tabla, **L** es poder leer, **E** poder cambiar, **C** poder crear y **B** poder borrar.

| Qué es | L | E | C | B |
|---|---|---|---|---|
| Contacto (clientes) | Sí | Sí | Sí | No |
| Pedido de venta | Sí | Sí | Sí | No |
| Producto | Sí | No | No | No |

Lucía puede ver y cambiar clientes y pedidos, y crear otros nuevos, pero no puede borrarlos. Los productos solo puede mirarlos.

## Pruebas: qué puede y qué no puede hacer cada uno

Entré en Odoo con cada persona y probé esto:

| Prueba | Persona | Qué pasa |
|---|---|---|
| Buscar el menú Facturación | Lucía | No aparece |
| Borrar un cliente | Lucía | No la deja |
| Ver presupuestos de otros compañeros | Lucía | Solo ve los suyos |
| Cambiar un producto | Lucía | No la deja |
| Ver todos los presupuestos | Carlos | Los ve todos |
| Dar salida a un pedido en Inventario | Carlos | Puede |
| Buscar el menú Facturación | Carlos | No aparece |
| Crear y publicar una factura | Ignacio | Puede |
| Registrar un cobro | Ignacio | Puede |
| Buscar el menú Inventario | Ignacio | No aparece |
| Entrar en los ajustes de Ventas | Ignacio | No tiene acceso |
| Ver documentos de otros clientes | Marta | Solo ve los suyos |
