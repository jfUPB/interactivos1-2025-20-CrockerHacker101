# Unidad 2

## 🛠 Fase: Apply 

# Actividad 01  
### **1. ¿Cómo funciona este ejemplo?**  

Este programa en MicroPython para micro:bit implementa una lógica de parpadeo independiente para dos pixeles de la matriz LED, utilizando una máquina de estados por cada píxel. 

Se define una clase `Pixel` que controla el comportamiento de un único LED ubicado en una posición específica (`pixelX, pixelY`). Cada instancia de esta clase alterna entre encender (valor 9) y apagar (valor 0) el pixel segun un intervalo de tiempo definido por el usuario. Esta lógica se ejecuta dentro de un bucle infinito mediante el método `update()`.

### **2. ¿Cuáles son los estados en el programa?**

  El programa dado por el script se divide en 2 estados:

- **Init**: Inicializa el tiempo de referencia (`startTime`) y muestra el estado inicial del pixel.  
- **WaitTimeout**: Espera a que pase el intervalo de tiempo para alternar el estado del píxel (encendido o apagado) y actualizar el tiempo de referencia.

 De esta manera, cada píxel parpadea de forma independiente en su propio intervalo de tiempo sin necesidad de interrupciones ni eventos externos.  

 ### **3. ¿Cuáles son los eventos/inputs en el programa?**  

este script no depende de un input como los botones o sensores ya que sus eventos internos es el paso del tiempo medido con `utime.ticks_ms()` y `utime.ticks_diff()`.  

### **4. ¿Cuáles son las acciones en el programa?**  

Las acciones que realiza cada objeto `Pixel` están definidas dentro del método `update()` y son las siguientes:

- **Inicializar el tiempo de referencia:**  
  Se guarda el tiempo actual utilizando `utime.ticks_ms()` cuando el estado es `"Init"`.

- **Encender o apagar el píxel:**  
  Se utiliza `display.set_pixel(x, y, valor)` para mostrar el estado del pixel en la matriz LED. El valor cambia entre `0` (apagado) y `9` (encendido).

- **Alternar el estado del brillo:**  
  Cuando ha pasado el intervalo de tiempo definido, el valor del pixel se alterna de 0 a 9.

- **Actualizar el tiempo de referencia nuevamente:**  
  Cada vez que se cambia el estado del pixel, se actualiza `startTime` para medir el siguiente intervalo correctamente.

- **Mantenerse en el estado `"WaitTimeout"`:**  
  Una vez inicializado, el objeto permanece en este estado ejecutando las acciones anteriores en cada ciclo de actualizacion.
