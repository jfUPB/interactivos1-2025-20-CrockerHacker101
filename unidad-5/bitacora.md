
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

4. que hace que se generen los evento A y B en p5.js
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
