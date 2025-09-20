
# Evidencias de la unidad 5

### Actividad 1

1: el micro:bit manda datos de los sensores de este, tales como los botones, el giroscopio. El uart.init permite que el microbit y el p5.js se puedan comunicar y las bibliotecas de p5.js que funcionen correctamente  

2: La estructura ASII usado es el siguiente:

lo que hace es micro:bit enviar los datos por UART/Serial en formato de texto plano (ASCII).
con la siguiete linea:
~~~
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
uart.write(data)
~~~

Eso significa que cada paquete que llega al computador es una cadena ASCII con esta estructura:
~~~
<xValue>,<yValue>,<aState>,<bState>\n
~~~
- xValue es el entero del acelerómetro en eje X  
- yValue es el entero del acelerómetro en eje Y  
- aState es el True o False según el botón A  
- bState es el True o False según el botón B  
- , es el separador de valores  
- \n es el indica fin de la línea (paquete)  

3: la parte dode se hace la lectura y transfromación de datos es en draw().   
- "Primero port.readUntil("\n")"  es el lee toda la linea eviada por el microbit.  
- "data.split(",")" es la que divide el codigo en 4 sensores del micro:bit que son (x, y, A, B)    
- "microBitX = int(values[0]) + windowWidth/2;" convierte el valor X a número entero y se le suma windowWidth/2 para que el centro de la pantalla sea el punto (0,0) del micro:bit.  
- "microBitY = int(values[1]) + windowHeight/2;" es lo mismo pero en y  
- microBitAState y microBitBState se convierten a booleanos (true/false)

4: que hace que se generen los evento A y B en p5.js
el evento A pressed detecta cuando el botón A pasa de false a true:
~~~
if (newAState === true && prevmicroBitAState === false)
~~~
esto es cuando se presiona   
el evento B released
Se detecta cuando el botón B pasa de true a false:
~~~
if (newBState === false && prevmicroBitBState === true)
~~~
Esto es cuando recien se suelta.

### reflexión:
Al enviar datos del micro:bit en formato ASCII, puedo entender fácilmente qué significa cada valor porque están separados y claros. Me gusta cómo en p5.js leo toda la línea, divido los datos y los convierto para que funcionen con la pantalla. Además, reconocer los cambios en los botones A y B me ayuda a controlar eventos importantes. Este ejercicio me hizo ver lo fundamental que es organizar bien los datos para que la comunicación entre dispositivos sea clara y efectiva.

5: capturas

![WhatsApp Image 2025-09-09 at 11 39 55 AM (2)](https://github.com/user-attachments/assets/ca2e0055-b3a6-4445-9fec-53eae0ec2b41)


![WhatsApp Image 2025-09-09 at 11 39 55 AM (1)](https://github.com/user-attachments/assets/763ab67b-1772-4312-a558-af79b0de0618)

![WhatsApp Image 2025-09-09 at 11 39 55 AM](https://github.com/user-attachments/assets/a8f0312d-022a-4019-92ea-71f8966e9766)


# Actividad 02

### 🧐🧪✍️ Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?  

<img width="1063" height="320" alt="image" src="https://github.com/user-attachments/assets/b1113b46-97bd-4a81-b5e6-2361c76b129e" />

Los datos binarios enviados desde el micro:bit no son legibles como texto porque están en formato compacto de bytes (struct.pack). En el SerialTerminal configurado en modo “Texto” se ven caracteres extraños, ya que el programa interpreta cada byte como un carácter ASCII. Para verlos correctamente, necesitamos un programa que los interprete como lo que son: enteros binarios (por ejemplo, en p5.js en la siguiente actividad).

###  🧐🧪✍️ Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?  

El resultado extraño que aparece en el monitor serial se debe a que ahora los datos se están enviando en formato binario, no en texto plano. La línea con struct.pack es la responsable de ese cambio: empaqueta los valores del acelerómetro y los botones en bytes, lo que hace la transmisión más eficiente pero también menos legible para nosotros.

<img width="1000" height="302" alt="image" src="https://github.com/user-attachments/assets/1dcc228b-6949-48de-b2b7-a28ba12c56d5" />

yo creo es más difícil de leer que el texto en ASCII, porque en ASCII veíamos directamente -345,678,1,0, mientras que en binario vemos secuencias como 0xFE 0xA7 0x02 0xA6 0x01 0x00, etc. que solo cobran sentido si un programa (como p5.js) las interpreta correctamente.

### 🧐🧪✍️ ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?  

- ASCII es ideal para probar, depurar y entender fácilmente lo que pasa en la comunicación.
- Binario es mejor cuando se busca eficiencia, velocidad y transmisión compacta, especialmente útil en aplicaciones con sensores que generan muchos datos o cuando hay limitaciones de ancho de banda.

### 🧐🧪✍️ Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

<img width="1001" height="307" alt="image" src="https://github.com/user-attachments/assets/dc95d5d0-e31b-4911-9f08-bf1482d8e789" />

cuando ajito el micro:bit, se envían 6 bytes:  

- Los primeros 2 bytes representan xValue.  
- Los siguientes 2 bytes representan yValue.  
- El quinto byte indica el estado del botón A (1 o 0).  
- El sexto byte indica el estado del botón B (1 o 0).  
- El formato >2h2B define esa estructura y garantiza que siempre se envíen los mismos 6 bytes en el mismo orden.

🧐🧪✍️ Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?  

las diferencias son las siguientes tanto ventajas como desventaja 

- En binario: compacto y rápido, pero ilegible directamente.  
- En ASCII: más largo y lento, pero fácil de leer y depurar.  
se suele usar ASCII para depuración y binario para aplicaciones finales donde importa la eficiencia.

### reflexión:
Al ver los datos en binario desde el micro:bit, entiendo que no son fáciles de leer porque están empaquetados con struct.pack para ser más eficientes y rápidos. En cambio, con ASCII podía ver los valores claramente, lo que facilitaba la depuración. Ahora sé que usaré ASCII para probar y entender mejor los datos, pero el formato binario es mejor para proyectos finales donde la velocidad y el ahorro de espacio son importantes. Esta experiencia me ayudó a entender cuándo usar cada formato según lo que necesite en mi proyecto.

### Actividad 03

🧐🧪✍️ Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

En la unidad anterior, al enviar datos como texto, necesitábamos separadores y un delimitador de fin de paquete (\n) para entender dónde terminaban los valores y el paquete, Ahora, al enviar datos como binarios estructurados de tamaño fijo, no necesitamos separadores ni delimitadores, porque el receptor puede leer bloques de 6 bytes directamente, sabiendo que cada uno es un paquete completo.

🧐🧪✍️ Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?  

El cambio más importante es que pasamos de leer y procesar texto delimitado a leer datos binarios estructurados con tamaño fijo, Esto hace que el código sea más rápido, más robusto y más preciso, eliminando la necesidad de separar cadenas o usar saltos de línea como delimitadores.  

- Lee exactamente 6 bytes.  
- Interpreta los valores según su tipo (int16, uint8, etc.).  
- Más eficiente y confiable.

🧐🧪✍️ ¿Qué ves en la consola? ¿Por qué crees que se produce este error?  

ete error en la consola se produce porque el código de p5.js está leyendo bloques de 6 bytes sin verificar si están alineados correctamente con los paquetes enviados por el micro:bit y como no usa delimitadores, encabezados o una verificación de integridad, es posible que p5.js lea desde la mitad de un paquete, lo cual desincroniza los datos y causa resultados erróneos como microBitX: 3073.

🧐🧪✍️ Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?  

los cambios son los siguientes
1. Framing en el micro:bit (emisor)  

- Envía un byte de inicio (0xAA).  
- Luego, 6 bytes con los datos: xValue, yValue, aState, bState.  
- Finalmente, 1 byte de checksum, que es la suma de los 6 bytes de datos módulo 256.  

2. Lectura robusta en p5.js (receptor)

- Los datos llegan al serialBuffer.  
- Busca siempre un byte de inicio (0xAA).  
- Verifica si hay 8 bytes completos.  
- Calcula y compara el checksum.  
- Solo si el paquete es válido, lo interpreta.  

🧐🧪✍️ Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?

Al iniciar el codigo sale el botón de conect to micro:bit, al conectar el micro:bit empieza a crear lineas que giran entorno a las manecillas del reloj, indefinida mente, puede ser modificada el grozor, largo, color etc, al presionar algunas teclas del teclado, pero el proyecto no reacciona con los botónes del micro:bit.

🧐🧪✍️ ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

Ahora para poder poner lineas se usa en micro:bit, usando el botón A se ponen las lineas en sentido a las manecillas de reloj, con el botón B se puede cambiar de color las lineas y dependiendo se du color cambian de tamaño, pero las teclas aún cumplen su función como el cambio de color con 1, 2, 3, 4 y 5 y con 6, 7, 8, 9 se cambia la forma de las lineas.

### reflexión:
Antes enviaba datos en texto con separadores y saltos de línea para identificar cada paquete, pero eso podía ser lento y propenso a errores. Ahora, al enviar datos binarios de tamaño fijo, no necesito delimitadores, lo que hace la comunicación más rápida y confiable, al principio tuve errores porque el receptor leía datos desalineados, pero al agregar un byte de inicio y un checksum pude sincronizar bien la comunicación y verificar la integridad de los datos, estos cambios mejoraron mucho la estabilidad y ahora el programa responde correctamente a los botones del micro:bit.

### Preguntas
1. por que tiene que ser si o si 115000 y no otro numero  
Porque tanto el micro:bit como p5.js deben tener la misma velocidad. Yo uso **115200** porque es rápida, estable y compatible con la mayoría de dispositivos. Si pongo otra, los datos llegan mal.  


2. ¿Qué gano usando binario?  
Gano velocidad y eficiencia. Se mandan menos bytes y todo es más rápido. Aunque no se entiende a simple vista, es mejor para programas finales.  

3. ¿Para qué sirve el byte de inicio y el checksum?  
El byte de inicio me ayuda a saber dónde empieza el paquete. El checksum me dice si el paquete llegó bien o se dañó. Así evito errores en los datos.  

 4. ¿Qué significa `>2h2B`?  
Significa que envío 2 enteros de 16 bits y 2 bytes, en orden big-endian. Así sé cómo leer bien los datos binarios en el mismo orden que los mandé.  

5. ¿Qué pasa si no leo los 6 u 8 bytes completos?  
Si leo menos, los datos se mezclan o se ven raros. Me sale que X vale 3000 o que el botón A está presionado cuando no lo está. Se rompe todo hasta que se alinea otra vez.  

6. ¿Cómo uso struct.pack?
Uso struct.pack para convertir los datos del micro:bit (como el acelerómetro y los botones) a formato binario. En mi caso uso struct.pack('>2h2B', x, y, a, b), que convierte dos enteros (x, y) y dos valores de 1 byte (botones A y B) en un paquete de 6 bytes. Así envío los datos de forma compacta.

7. ¿Cuántos bytes ahorro usando binario y por qué se produce el error de sincronización?
Con ASCII los paquetes ocupaban alrededor de 13 bytes, pero con binario solo uso 6 bytes, así que ahorro casi la mitad del espacio, el error de sincronización pasa porque el receptor puede leer desde la mitad de un paquete, ya que en binario no hay delimitadores como el salto de línea. Por eso se agregan cosas como byte de inicio y checksum, para asegurarse de que se lea el paquete completo y correcto.

8. ¿Qué otras estrategias de framing existen y cuáles son sus ventajas?
Además del byte de inicio + checksum, también se puede usar:  

- Un encabezado con longitud de datos (útil para mensajes de tamaño variable)  
- Códigos especiales como STX/ETX para marcar inicio y fin (más usados en texto)  
- Protocolos como SLIP o COBS que son más avanzados para binario  
- Estas estrategias ayudan a que el receptor sepa dónde empieza y termina cada paquete, y a evitar errores.  

9. ¿Cuándo prefiero usar ASCII en lugar de binario?
Aunque binario es más rápido y eficiente, usar ASCII tiene ventajas cuando estoy:  

Probando o depurando el sistema  
- Trabajando en prototipos  
- En proyectos educativos o de baja velocidad   
- Es más fácil de leer y entender, aunque ocupa más espacio.

10. ¿Por qué es importante implementar un byte de inicio y un checksum en la comunicación serial binaria?   
Para mí es muy importante usar un byte de inicio y un checksum porque, al enviar datos en formato binario, no hay delimitadores visibles como en ASCII, y eso puede hacer que mi programa empiece a leer datos desde medio paquete, lo que genera errores, el byte de inicio (por ejemplo, 0xAA) me ayuda a identificar dónde comienza cada paquete, así puedo sincronizar la lectura correctamente, el checksum me permite verificar si los datos llegaron bien, porque hago la suma de los bytes y la comparo con el valor recibido con esto, sólo proceso paquetes completos y sin errores, lo que hace que la comunicación sea mucho más confiable.

Nota: 4.0
yo digo que un 4 ya que:  
- mi profundidad de indagación es la adecuada, hago las preguntas adecuadas para el proyecto.    
- aunque no tengo ningun experimento propio cumplí con las preguntas de la bitacora y le añadí una reflexión de lo que entendí y aprendí durante el proceso de las actividades.  
- siento que mi comprención de los temas abarcados en esta unidad son claramente explicados durante las actividades de la unidad.  
