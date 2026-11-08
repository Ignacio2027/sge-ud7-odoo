# Problemas al instalar Odoo 19 (Lúpulo Errante S.L.)

Instalé Odoo 19 gratuito con Docker. Se abre en `http://localhost:8069`. La base de datos se llama `lupuloerrante`(no hacia falta crear base de datos y no la he creado) y no tiene datos de ejemplo.

No me salió ningún problema por sí solo. Por eso hice dos cosas:

1. Revisé todo antes de empezar.
2. Provoqué a propósito tres problemas típicos y los arreglé.

## 1. Lo que revisé antes de empezar

| Qué revisé | Cómo | Qué tenía que salir |
| Que Docker está instalado | `docker --version` | Sale un número de versión |
| Que Docker Compose está instalado | `docker compose version` | Sale un número de versión |
| Que Docker está encendido | `docker ps` | No da error |
| Que el puerto 8069 está libre (Windows) | `netstat -ano \| findstr 8069` | No sale nada |
| Que el puerto 8069 está libre (Mac o Linux) | `lsof -i :8069` | No sale nada |
| Memoria del ordenador | Administrador de tareas | Al menos 4 GB |
| Espacio libre | Explorador de archivos | Al menos 10 GB |

El puerto es como una puerta del ordenador. Odoo usa la puerta 8069, y si otro programa ya la está usando, Odoo no puede entrar.

## 2. Problemas que provoqué y arreglé

| Qué salió | Por qué pasó | Cómo lo arreglé | Dónde lo consulté |
| `port is already allocated` (el puerto ya está en uso) | Otro programa estaba usando la puerta 8069 | Cerré ese programa con `docker stop ocupa` y `docker rm ocupa` y volví a encender Odoo con `docker compose up -d`. Otra opción: usar otra puerta, la 8070 | Ayuda de Docker; IA: Claude (Anthropic) |
| El navegador dice «Internal Server Error» (error interno del servidor) | La base de datos estaba apagada y Odoo no podía guardar ni leer nada | Miré los mensajes con `docker compose logs odoo`, vi que no conectaba y encendí la base de datos con `docker compose start db` | Ayuda de Odoo; IA: Claude (Anthropic) |
| `password authentication failed` (la contraseña no es correcta) | Odoo y la base de datos tenían contraseñas distintas | Puse la misma contraseña en los dos sitios y volví a encender todo | Ayuda de Odoo; IA: Claude (Anthropic) |

## 3. Cómo provoqué cada problema

**Puerto ocupado**
1. Ocupé la puerta 8069 con otro programa: `docker run -d --name ocupa -p 8069:80 nginx`.
2. Intenté encender Odoo con `docker compose up -d` y salió el error.
3. Cerré el otro programa con `docker stop ocupa` y `docker rm ocupa`.
4. Volví a encender Odoo y la página abrió bien.

**Base de datos apagada**
1. Con Odoo funcionando, apagué la base de datos: `docker compose stop db`.
2. Recargué la página y salió el error.
3. Miré los mensajes: `docker compose logs odoo`.
4. Encendí la base de datos: `docker compose start db`, y recargué.

**Contraseñas distintas**
1. Cambié la contraseña de Odoo para que no fuera igual a la de la base de datos.
2. Encendí con `docker compose up -d` y miré los mensajes: `docker compose logs db`.
3. Puse las dos contraseñas iguales y volví a encender.

## 4. Uso de IA

Usé la IA (Claude) solo para entender estos problemas y por qué pasan, como permite la práctica. La empresa, los documentos y la práctica son míos.

Las capturas de cada problema y de su solución están en la carpeta `capturas/`.
