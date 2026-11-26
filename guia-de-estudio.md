# Guía de estudio — API testing con Postman

**Para Modo. En simple, para defenderlo en una entrevista en vivo.**

## Las 4 ideas (en simple)

### 1. Una API es un mesero
La app no habla directo con la base de datos. Pide cosas a un **servidor** por una **API**: una dirección (endpoint) + un verbo (método).
- **GET** = leer (dame los usuarios).
- **POST** = crear (crea un post nuevo).
- **PUT** = actualizar (cambia el post 1).
- **DELETE** = borrar (borra el post 1).
- Ejemplo: `GET https://jsonplaceholder.typicode.com/users/1` = "dame el usuario 1".

### 2. El código de estado dice qué pasó
- **200** = salió bien. **201** = creado (POST exitoso).
- **400** = petición mala (faltan datos o están mal).
- **401** = sin autorización (falta token o credenciales).
- **404** = no existe (usuario 999, ruta inventada).
- **500** = error del servidor (culpa de ellos, no tuya).
- Regla: un test que solo mira el 200 está incompleto. El buen QA prueba también el 400, el 401 y el 404.

### 3. Un test de API verifica 4 cosas
1. **Status** — ¿llegó el código esperado?
2. **Cuerpo** — ¿los datos son los que pedí? (el título, el id, el userId).
3. **Forma (esquema)** — ¿cada campo existe y es del tipo correcto? (email es texto y tiene @, id es número).
4. **Contenido conocido** — ¿los datos fijos son los que deben ser? (el primer usuario es Leanne Graham, un dato fijo de esta API de demo). El tiempo de respuesta también se puede medir, pero un límite fijo (ej. 2000 ms) falla cuando la red está lenta aunque la API esté bien: eso es un test inestable (*flaky*), y un QA no lo deja así.
- En Postman eso se escribe en la pestaña **Tests** con `pm.test(...)`.

### 4. Variables y colecciones: no repitas la URL
- La **colección** es el plan de pruebas ejecutable: 14 peticiones con sus tests.
- El **entorno** guarda las URLs base como variables: `{{baseUrlPlaceholder}}`, `{{baseUrlHttpbin}}`.
- Si la API cambia de servidor, cambias UNA variable, no 14 peticiones. Eso es lo que hace un QA ordenado.

## Preguntas típicas de entrevista (con respuesta corta)

**¿Qué es una API REST?**
Una forma de pedir datos a un servidor por HTTP: una dirección (endpoint) y un método (GET, POST, PUT, DELETE). La respuesta viene en JSON con un código de estado.

**¿Qué significan 200, 201, 400, 401, 404 y 500?**
200 salió bien; 201 creado; 400 petición mala; 401 sin autorización; 404 no existe; 500 error del servidor.

**¿Cómo pruebas un endpoint sin documentación?**
Primero el camino feliz (GET y su 200), luego los bordes: id que no existe (404), sin token (401), datos incompletos (400), y verifico que el cuerpo tenga los campos que la app necesita.

**¿Qué es un test de contrato o esquema?**
Verificar que la respuesta siempre tenga los mismos campos con los mismos tipos. Si la app espera `email` y un día falta, la app se rompe. Mi petición 14 hace eso con los 10 usuarios.

**¿Cómo reportas un bug de API?**
Con: petición exacta (método + URL + cuerpo), lo esperado, lo real (status y cuerpo), y pasos para repetirlo. Sin "no funciona".

**¿Qué haces si un test pasa a veces y falla otras?**
Primero miro si es el tiempo de respuesta (red lenta) o un dato que cambia (id aleatorio). No lo marco como pasado a mano: lo investigo y lo dejo estable o lo reporto.

## 3 ejercicios (sin mirar la colección)

1. Corre la colección completa en Postman o con Newman. Tiene que dar 14 peticiones y 27 verificaciones en verde, 0 fallos.
2. Rompe un test a propósito: en "GET All users" cambia la verificación de 200 a 201, corre solo esa petición y lee el fallo. Luego devuélvelo a 200. Eso te enseña a leer fallos.
3. Añade una petición nueva: `GET {{baseUrlPlaceholder}}/comments?postId=1` con 2 verificaciones (status 200 y que cada comentario tenga `postId` igual a 1). Si la haces, ya sabes crear tests, no solo correrlos.

## Cómo defenderlo en vivo (cuando llegue la entrevista)

1. Abre Postman, muestra la colección: 2 carpetas, 14 peticiones, cada una con sus tests.
2. Corre toda la colección y muestra los 25 checks en verde.
3. Explica el caso que más impresiona: el 404 del usuario 999 y el 401 sin token — "no solo probé lo que funciona, probé lo que debe fallar".
4. Explica las variables de entorno: "si cambia el servidor, cambio una variable".
5. Di la verdad: "Es práctica con APIs públicas de demo (JSONPlaceholder y httpbin), mientras aprendo API testing. Los datos son sintéticos, no reales. Lo que sí es real: las peticiones, las verificaciones y que corren en verde."
6. Si preguntan por algo que no sabes: "Eso todavía no lo he hecho, pero sé dónde está en la colección y lo aprendo en la semana del proceso." Nunca inventes un skill.
