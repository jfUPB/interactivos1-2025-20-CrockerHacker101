
# Evidencias de la unidad 7

# Actividad 1  

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?  

lo que pasa con la URL que nos da el node es que solo nos sirve en el mismo pc, osea que no se comparte con otros y si pones esa URL en otro PC o dispositivo mobil no la va a encontrar.  

### Describe brevemente qué hace npm install y npm start.  

npm install descarga unos componentes llamados y a la carpeta donde esta el proyecto, esto es para que el server funcione correctamente, si no se le instala estos componentes, el node no va a encontrar el server.  

npm start es pa prender el server, y que funcione y cree la URL, tambien se puede iniciar con node "server.js".  

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

<img width="1572" height="348" alt="Captura de pantalla 2025-10-07 111146" src="https://github.com/user-attachments/assets/aa6d892c-d21f-46aa-b93e-ddc1d63d7fa7" />

<img width="1564" height="104" alt="Captura de pantalla 2025-10-07 111236" src="https://github.com/user-attachments/assets/9f486fac-7236-4107-88d5-bbfd367333c0" />

 ### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?  

si que funcionó, salio una bolita en el pcerdo, y en mi cell salio "touch to move" o algo asi y al tocar por ese recuadro podia mover la bolita de la pantalla del pc, aun que habia un poco de delay no era molesto.  

# Actividad 2  

### ¿Por qué es necesario Dev Tunnels y cómo funciona?

Dev Tunnels es necesario porque localhost solo es accesible desde tu propio computador, no desde otro dispositivo como un celular. Dev Tunnels crea un enlace público seguro que conecta una URL accesible en Internet directamente con tu servidor local en el puerto 3000, permitiendo que cualquier dispositivo acceda a tu app aunque no esté en la misma red.

### ¿Qué hace touchMoved() y para qué sirve el threshold?

touchMoved() detecta cuando el usuario mueve el dedo sobre la pantalla y obtiene las coordenadas del toque en tiempo real. El threshold evita enviar datos por cada pequeño movimiento, solo manda información si el dedo se mueve lo suficiente, para no saturar la red y mejorar el rendimiento.

### Comparación: Dev Tunnels vs IP local

- Dev Tunnels: Permite acceso desde cualquier red, es seguro y funciona con una URL pública, pero depende de un servicio externo.  
- IP local: Solo funciona en la misma red Wi-Fi, es más simple pero no accesible desde fuera y menos seguro.  

### Capturas 
<img width="739" height="1258" alt="499416538-62e977a0-10f7-4721-a4a3-354ad0965224" src="https://github.com/user-attachments/assets/9e917d77-a8ed-4303-897e-fcba3fa18286" />


<img width="1920" height="1080" alt="499416301-162a6b93-bd68-4b2a-b6ee-710602e1c01d" src="https://github.com/user-attachments/assets/ece663c7-31f2-403c-84c9-de99d368410b" />


# Actividad 3  

### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?  

express.static('public') sirve para servir archivos estáticos automáticamente desde la carpeta public. Eso incluye HTML, CSS, imágenes, JS del lado del cliente, etc.  
como si tuviera un archivo en "public/index.html", puedes acceder a él simplemente desde "http://localhost:3000/index.html" sin necesidad de definir una ruta manualmente.  

en comparación:  
- ### express.static(...) es automático y genérico, útil para servir muchos archivos sin declarar cada ruta.###  
- ### app.get('/ruta', ...) es manual y específico, se usa cuando quieres controlar lo que pasa en una ruta particular (por ejemplo, devolver JSON, redirigir, manejar lógica, etc.).###  

### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?  

flujo:  

Desde el móvil:
Se emite un mensaje usando
socket.emit('message', datos)
(por ejemplo, al mover el dedo en la pantalla).

Servidor (backend):
Recibe ese mensaje con
socket.on('message', callback)
y luego lo reenvía a otros clientes usando
socket.broadcast.emit('message', datos).

Hacia el escritorio:
Los escritorios (u otros clientes) escuchan
socket.on('message', callback)
y reaccionan (por ejemplo, moviendo algo en pantalla).

¿Por qué usar broadcast?
Porque así el móvil no recibe su propio mensaje, solo lo reciben los demás.

### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?  

ambos pc´s recibirían el mensaje.

Por qué?
Porque el servidor usa: "socket.broadcast.emit('message', message);"  
Lo cual envía el mensaje a todos los clientes conectados excepto al móvil que lo emitió. Por eso, los escritorios sí lo reciben, pero el móvil no.  

### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?  

- Ver que el servidor está recibiendo eventos.  
- Depurar errores.  
- Asegurar que todo está funcionando como esperas.  

# Actividad 4  
Flujo de datos entre Móvil, Servidor y Escritorio (Socket.IO)  

Este diagrama muestra cómo el toque en el cliente móvil viaja a través del servidor hasta el cliente de escritorio, usando Socket.IO. Se ejemplifica con coordenadas táctiles (x, y).  

1.1. Cliente móvil (mobile/sketch.js): El usuario toca la pantalla. Se capturan las coordenadas x=120, y=250 y se envían al servidor con socket.emit('touch', {x:120, y:250}).  
2.2. Servidor (server.js): Escucha el evento 'touch' y reenvía los datos a todos los clientes con io.emit('draw', data).  
3.3. Cliente de escritorio (desktop/sketch.js): Escucha el evento 'draw' y dibuja un punto o figura en las coordenadas recibidas.  
resumen de eventos Socket.IO  

Etapa	Actor	Acción	Evento Socket.IO  
1.	Cliente móvil	Captura toque y envía coordenadas	socket.emit('touch', {x, y})  
2.	Servidor	Recibe datos y los reenvía	socket.on('touch') → io.emit('draw')  
3.	Cliente escritorio	Recibe coordenadas y dibuja	socket.on('draw', data)  

diagrama:  

<img width="917" height="333" alt="image" src="https://github.com/user-attachments/assets/9fa63a39-e9c1-4619-ac38-2668779ab55b" />

# Actividad 5



