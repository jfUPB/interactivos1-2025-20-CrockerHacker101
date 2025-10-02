
# Evidencias de la unidad 6

## 🧐🧪✍️ Reporta en tu bitácora

### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

- primero pase la bitacora del profo a mi pc personal (en este caso el de la U) para poder trabajar mas tranquilo.

<img width="597" height="394" alt="MINGW64__c_Users_B09S113est_Documents_entangledTest-sfi1-2025-20                                                   23_09_2025 10_58_52 a  m" src="https://github.com/user-attachments/assets/647618b2-3906-41ea-ad61-cfc9cbe23bbc" />


- despues le instale el "npm" al git bash y me salio lo siguiente en la terminal: 

<img width="1110" height="736" alt="image" src="https://github.com/user-attachments/assets/abd40201-4e75-4466-90a7-a27b4afdc6bb" />

<img width="610" height="417" alt="image" src="https://github.com/user-attachments/assets/dfa29c4f-a388-40d1-84f7-aa2cd939c653" />

- el proposito de esto es que, en la terminal de Git Bash al ejecutar npm start es informarme el estado del servidor Node.js que se esta ejecutando, asi como sobre la conexión y sincronización de varios clientes que se conectan a él.  

### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?   

el mensaje que salio fue:  
```
> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000
```  
este mensaje significa que el servidor Node.js se inició correctamente y esta escuchando en http://localhost:3000, listo para recibir conexiones.  
### Describe lo que ves inicialmente en page1 y page2 en tu navegador.  

- despues use el link dado por el "NPM" se pudo abrir unos proyectos que al abrir 2 ventanas distintas que se "conectan" una con otra, salieron una especie de bolitas unidas con cuerdas, que, estas se "siguen" atravez de toda la pantalla como si estubieran conectadas a pesar de estar estar en distintas ventanas, lo que me salio fue lo siguiente:

<img width="1794" height="1022" alt="image" src="https://github.com/user-attachments/assets/f48f6285-c26c-43dd-910d-b1749a588a18" />

# Actividad 2

# ¿Qué pasaría si se corta tu acceso a Internet?

Cuando te conectas a Internet en casa o en la universidad, usas una “rampa de acceso” como el Wi-Fi o un cable de red. Pero, ¿qué ocurre si esa rampa se corta?:
Consecuencias inmediatas

- **Pérdida de acceso a servicios en línea**    
  No se puede navegar por páginas web ni ingresar a plataformas como Moodle, Google Classroom, entre otras.  

- **Aplicaciones en la nube dejan de funcionar**    
  Servicios como Google Drive, Dropbox o OneDrive no se sincronizan. Tampoco se puede acceder a plataformas como Spotify, Netflix o YouTube si no hay contenido descargado.  

- **Interrupción de la comunicación**   
  No se pueden enviar mensajes por WhatsApp, Telegram o correo electrónico. Las redes sociales no estarán disponibles.  

Consecuencias a largo plazo  

- **Retrasos en trabajo o estudios**    
  No se pueden enviar tareas, participar en clases virtuales ni cumplir con plazos importantes.  
  
- **Dependencia tecnológica evidente**    
  Se vuelve evidente cuánto dependemos del acceso a Internet para realizar tareas cotidianas.  

- **Falta de información en tiempo real**   
  No es posible consultar noticias, actualizaciones, el clima o resolver dudas rápidamente.    

Reflexión final  

La conexión a Internet, ya sea mediante Wi-Fi o cable de red, es más que una herramienta: es un puente hacia el conocimiento, la comunicación y la colaboración. Cuando se interrumpe, quedamos temporalmente aislados del ecosistema digital.    
Esto resalta la importancia de contar con planes de contingencia y alternativas ante posibles desconexiones.  

# Relación Cliente-Servidor en la Vida Diaria
Modelo Cliente-Servidor

En el mundo digital, el navegador web (Chrome, Firefox, Safari, Edge…) actúa como un Cliente: solicita información y muestra los resultados al usuario. El Servidor, por su parte, es quien entrega la información solicitada.

**Base del modelo:**
- El Cliente pide.
- El Servidor responde.

Este modelo también puede observarse en situaciones cotidianas fuera del entorno digital.

## Ejemplos de Cliente-Servidor en la Vida Diaria

### 1. Restaurante
- **Cliente:** Persona que entra al restaurante y hace un pedido.
- **Servidor:** Mesero o cocinero que recibe el pedido y entrega la comida.
- **Lo que se pide:** Un platillo del menú.
- **Lo que se entrega:** El platillo solicitado.

### 2. Biblioteca
- **Cliente:** Persona que solicita un libro.
- **Servidor:** Bibliotecario o sistema de préstamos.
- **Lo que se pide:** Un libro específico.
- **Lo que se entrega:** El libro para lectura o préstamo.

### 3. Tienda o supermercado
- **Cliente:** Persona que busca productos para comprar.
- **Servidor:** Cajero o sistema de autoservicio.
- **Lo que se pide:** Productos específicos.
- **Lo que se entrega:** Los productos y el recibo de compra.

### 4. Farmacia
- **Cliente:** Persona que entrega una receta médica.
- **Servidor:** Farmacéutico.
- **Lo que se pide:** Medicamentos específicos.
- **Lo que se entrega:** Medicamentos solicitados.

### 5. Transporte público
- **Cliente:** Pasajero que solicita un viaje.
- **Servidor:** Conductor o sistema de transporte.
- **Lo que se pide:** Un traslado a un destino.
- **Lo que se entrega:** El servicio de transporte.

## URL  

### URL usada: https://www.youtube.com/watch?v=dvgZkm1xWPE&list=RDEMuf6htoZivPnz-ZIwGU0dDA&index=10  

- El protoco es el "https://", como tiene una "S" quiere decir que es segura.  
- El nombre del dominio es "www.youtube.com"    
- La ruta es "/watch"  

Si en el navegador pongo solo el "www.youtube.com" este automáticamente se cambiara por "https://www.youtube.com", en ese caso el servidor YouTube decide que página “por defecto” mostrar bajo ese dominio raíz.
en este caso es la home page.

## HTTP  
### Comparación entre HTTP y protocolos seriales

HTTP y los protocolos seriales como los que se usan con el **micro:bit** tienen algunas similitudes, ya que ambos transmiten datos en forma de bytes y requieren un emisor y un receptor que estén de acuerdo en ciertas reglas básicas para que el mensaje sea entendido. En ambos casos existe un protocolo: en serial se define la **velocidad en baudios** y los **bits de datos**, mientras que en HTTP se define la estructura del mensaje con **métodos**, **cabeceras** y **cuerpo**.  

Sin embargo, hay diferencias clave:  
- El **protocolo serial** es de **bajo nivel** y se limita a enviar bytes en orden, sin un formato fijo; es una comunicación directa *1 a 1* entre dispositivos.  
- **HTTP** es un protocolo de **alto nivel** que se construye encima de TCP/IP y organiza la información en mensajes estructurados, diseñados para transferir recursos en la web (páginas, imágenes, videos) con **metadatos**, **autorización**, **idiomas** y muchas otras funciones.  
- Mientras que el serial solo conecta dos dispositivos, HTTP está pensado para **escalar a millones de clientes y miles de servidores** en todo el mundo.  

HTTP necesita ser más complejo que un simple envío de bytes porque en Internet no basta con transmitir datos crudos: hay que especificar qué recurso se solicita, en qué formato, si se permite almacenar en caché, si el usuario está autenticado, entre otros detalles. Esto hace que cliente y servidor puedan comunicarse de manera confiable y universal en un entorno muy variado, a diferencia del entorno controlado y directo que se tiene con una conexión serial en un micro:bit.  

## JAVA, HTML, CSS  
***HTML: es la estructura, lo que realmente existe en la página.***  

- Los campos de texto para “usuario” y “contraseña”.  
- El botón para “Iniciar sesión”.  
- Las etiquetas <form>, <input>, <button>.  
- En resumen: lo que define qué elementos hay en la página.  

***CSS: es la apariencia, cómo se ven esos elementos.***

- El color del botón (azul, verde, rojo…).  
- El tipo de letra y el tamaño del texto.  
- Los márgenes, bordes redondeados, sombras, fondo de la página.  
- En resumen: lo que da estilo y presentación al HTML.  

***JavaScript: es la interactividad, lo que ocurre cuando haces acciones.***

- Revisar que no envíes el formulario vacío.  
- Mostrar un mensaje de “contraseña incorrecta” sin recargar toda la página.  
- Hacer que el botón se bloquee después de varios intentos fallidos.  

## Comparación:  

El bucle draw() de p5.js funciona repitiéndose unas 60 veces por segundo, ejecutando código incluso cuando nada cambia. Esto es ideal en animaciones o juegos, donde la pantalla se actualiza constantemente. En cambio, el modelo basado en eventos de JavaScript en la web solo ejecuta funciones cuando ocurre algo (como un clic o una respuesta del servidor). Esto lo hace mucho más eficiente para interfaces de usuario, porque no desperdicia recursos redibujando la página innecesariamente, ahorrando CPU y batería.

## Usar Java  

### Ventajas de usar JavaScript en cliente y servidor

Con **Node.js** es posible usar JavaScript tanto en el navegador (cliente) como en el servidor.  
Antes se usaba JavaScript solo en el cliente y otro lenguaje distinto en el backend (como PHP, Java o Python).  
Unificar el lenguaje trae varias ventajas:

Principales ventajas
- **Unificación del lenguaje**: todo el proyecto se desarrolla en JavaScript, reduciendo la complejidad.  
- **Reutilización de código**: funciones como validaciones o utilidades pueden compartirse entre cliente y servidor.  
- **Mayor productividad**: no hace falta aprender varios lenguajes, lo que acelera el desarrollo.  
- **Trabajo en equipo más flexible**: los desarrolladores pueden moverse entre frontend y backend (rol *fullstack*).  
- **Mantenimiento más sencillo**: un solo lenguaje hace que el código sea más consistente y fácil de actualizar.  

## Resume con tus propias palabras  

La principal diferencia es que el "http" tradicional funciona tipo petición/respuesta el cliente siempre tiene que pedir algo y el servidor responde, algo como enviar un correo cada vez que necesitas información.
Con WebSockets/Socket.IO hay una conexión hay una conección permanentemente abierta, osea, que se pueden enviar mensajes en cualquier momento sin necesidad de repetir peticiones.  

Este tipo de comunicación se usa en:   
- Chats y mensajería en línea.  
- Juegos multijugador en tiempo real.  
- Aplicaciones colaborativas como Google Docs o pizarras compartidas.    
- Notificaciones instantáneas de aplicaciones web o móviles.  

# Actividad 3  



# Actividad 5  
"Caca" – Brainstorming Colaborativo en Tiempo Real

Objetivo:

Permitir a varios usuarios colaborar en tiempo real para generar ideas, organizar lluvias de ideas, agrupar temas, votar por las mejores ideas, y construir mapas mentales visuales desde distintas ubicaciones.

Ideal para:  

- Equipos creativos.  
- Estudiantes trabajando en proyectos.  
- Dinámicas de grupo remotas o presenciales.  

¿Qué la hace diferente?  
- Interactividad en tiempo real entre múltiples usuarios.   
- Cada idea es una “burbuja” que se puede arrastrar y soltar.   
- Ideas se pueden conectar visualmente con líneas (como un mapa mental).   
- Los usuarios pueden votar (likes), y las ideas más votadas cambian de color o tamaño.   
- Posibilidad de agrupar ideas dentro de categorías visuales.  
- Vista compartida en tiempo real (todos ven lo mismo en sincronía).   

Tecnología utilizada:  
- Node.js con Express.    
- Socket.IO para comunicación en tiempo real.  
- HTML5 + CSS3 + Vanilla JS (o opcionalmente algún framework frontend como Vue/React si se desea escalar).  
- Canvas API o SVG para la representación visual de ideas conectadas.  

<img width="469" height="280" alt="image" src="https://github.com/user-attachments/assets/a2f231a3-e356-49fb-abef-73b5adc5c339" />




