
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
Esto es cuando recien se suelta

# Actividad 02

### 🧐🧪✍️ Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?  

Los datos binarios enviados desde el micro:bit no son legibles como texto porque están en formato compacto de bytes (struct.pack). En el SerialTerminal configurado en modo “Texto” se ven caracteres extraños, ya que el programa interpreta cada byte como un carácter ASCII. Para verlos correctamente, necesitamos un programa que los interprete como lo que son: enteros binarios (por ejemplo, en p5.js en la siguiente actividad).

###  🧐🧪✍️ Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?  

El resultado extraño que aparece en el monitor serial se debe a que ahora los datos se están enviando en formato binario, no en texto plano. La línea con struct.pack es la responsable de ese cambio: empaqueta los valores del acelerómetro y los botones en bytes, lo que hace la transmisión más eficiente pero también menos legible para nosotros.

Sí, definitivamente es más difícil de leer que el texto en ASCII, porque en ASCII veíamos directamente -345,678,1,0, mientras que en binario vemos secuencias como 0xFE 0xA7 0x02 0xA6 0x01 0x00, que solo cobran sentido si un programa (como p5.js) las interpreta correctamente.

### 🧐🧪✍️ ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?  

- ASCII es ideal para probar, depurar y entender fácilmente lo que pasa en la comunicación.
- Binario es mejor cuando se busca eficiencia, velocidad y transmisión compacta, especialmente útil en aplicaciones con sensores que generan muchos datos o cuando hay limitaciones de ancho de banda.

### 🧐🧪✍️ Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

Cada vez que ocurre un shake, se envían 6 bytes:  

- Los primeros 2 bytes representan xValue.  
- Los siguientes 2 bytes representan yValue.  
- El quinto byte indica el estado del botón A (1 o 0).  
- El sexto byte indica el estado del botón B (1 o 0).  
- El formato >2h2B define esa estructura y garantiza que siempre se envíen los mismos 6 bytes en el mismo orden.

🧐🧪✍️ Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?  

El experimento muestra que el mismo dato puede representarse de dos formas:  

- En binario: compacto y rápido, pero ilegible directamente.  
- En ASCII: más largo y lento, pero fácil de leer y depurar.  
se suele usar ASCII para depuración y binario para aplicaciones finales donde importa la eficiencia.


### Actividad 03

🧐🧪✍️ Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

En la unidad anterior, al enviar datos como texto, necesitábamos separadores y un delimitador de fin de paquete (\n) para entender dónde terminaban los valores y el paquete, Ahora, al enviar datos como binarios estructurados de tamaño fijo, no necesitamos separadores ni delimitadores, porque el receptor puede leer bloques de 6 bytes directamente, sabiendo que cada uno es un paquete completo.

🧐🧪✍️ Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?  

El cambio más importante es que pasamos de leer y procesar texto delimitado a leer datos binarios estructurados con tamaño fijo, Esto hace que el código sea más rápido, más robusto y más preciso, eliminando la necesidad de separar cadenas o usar saltos de línea como delimitadores.  

- Lee exactamente 6 bytes.  
- Interpreta los valores según su tipo (int16, uint8, etc.).  
- Más eficiente y confiable.

🧐🧪✍️ ¿Qué ves en la consola? ¿Por qué crees que se produce este error?  

El error en la consola se produce porque el código de p5.js está leyendo bloques de 6 bytes sin verificar si están alineados correctamente con los paquetes enviados por el micro:bit. Al no usar delimitadores, encabezados o una verificación de integridad, es posible que p5.js lea desde la mitad de un paquete, lo cual desincroniza los datos y causa resultados erróneos como microBitX: 3073.

🧐🧪✍️ Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?  

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
