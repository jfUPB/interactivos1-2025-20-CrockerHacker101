
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


