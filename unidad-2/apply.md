# Unidad 2

## 🛠 Fase: Apply 

# Actividad 03 
### Concurrencia en este programa
Este programa permite realizar varias tareas **de forma concurrente** porque:
- **Secuencia automática de imágenes:** el micro:bit cambia de `HAPPY` → `SMILE` → `SAD` → `HAPPY` siguiendo intervalos de tiempo predefinidos.
- **Reacción inmediata a eventos externos:** si se presiona el botón A, la imagen cambia de inmediato sin esperar a que termine el intervalo.

En otras palabras, **la máquina de estados monitorea continuamente**:
1. El paso del tiempo (`utime.ticks_diff()`).
2. Las pulsaciones de botón (`button_a.was_pressed()`).

###  Estasdos, eventos y acciones

**Estados (state):**
- `STATE_INIT`: Estado inicial antes de mostrar la primera imagen.
- `STATE_HAPPY`: Cara feliz (`Image.HAPPY`).
- `STATE_SMILE`: Cara sonriente (`Image.SMILE`).
- `STATE_SAD`: Cara triste (`Image.SAD`).

**Eventos (event):**
- **Temporizador vence:** cuando el tiempo actual menos `start_time` supera `interval`.
- **Botón A presionado:** detectado con `button_a.was_pressed()`.

**Acciones (action):**
- Mostrar imagen (`display.show(...)`).
- Actualizar tiempo de inicio (`start_time = utime.ticks_ms()`).
- Definir nuevo intervalo de espera (`interval = ...`).
- Cambiar al nuevo estado (`current_state = ...`).


###  vectores de prueba

 **Vector 1: Cambio por tiempo en estado HAPPY**
- **Condiciones iniciales:**  
  Estado = `STATE_HAPPY`  
  Tiempo transcurrido = 1500 ms  
  Botón A = no presionado  
- **Evento:**  
  Temporizador vence.  
- **Resultado esperado:**  
  Mostrar `Image.SMILE`, intervalo = 1000 ms, estado = `STATE_SMILE`.  
- **Resultado obtenido:**

**Vector 2: Cambio inmediato por botón en estado SMILE**
- **Condiciones iniciales:**  
  Estado = `STATE_SMILE`  
  Tiempo transcurrido = < 1000 ms  
  Botón A = presionado  
- **Evento:**  
  Botón presionado antes de que acabe el tiempo.  
- **Resultado esperado:**  
  Mostrar `Image.HAPPY`, intervalo = 1500 ms, estado = `STATE_HAPPY`.  
- **Resultado obtenido:**

**Vector 3: Cambio por botón en estado SAD**
- **Condiciones iniciales:**  
  Estado = `STATE_SAD`  
  Tiempo transcurrido = < 2000 ms  
  Botón A = presionado  
- **Evento:**  
  Pulsar botón A.  
- **Resultado esperado:**  
  Mostrar `Image.SMILE`, intervalo = 1000 ms, estado = `STATE_SMILE`.  
- **Resultado obtenido:**



# Actividad 04   
Diseña la máquina de estados que solucione este problema: En un escape room se requiere construir una aplicación para controlar una bomba temporizada. El circuito de control de la bomba está compuesto por cuatro sensores, denominados UP (botón A), DOWN (botón B), touch (botón de touch) y ARMED (el gesto de shake de acelerómetro). Tiene dos actuadores o dispositivos de salida que serán un display (la pantalla de LEDs) y un speaker.  

### punto 1  





### punto 2   

```
from microbit import *
import utime

# Estados
CONFIG, ARMED, EXPLOSION = 0, 1, 2

# Variables
time_left = 20
state = CONFIG
last_tick = utime.ticks_ms()

while True:
    if state == CONFIG:
        display.show(str(time_left))
        if button_a.was_pressed() and time_left < 60:
            time_left += 1
        if button_b.was_pressed() and time_left > 10:
            time_left -= 1
        if accelerometer.was_gesture("shake"):
            last_tick = utime.ticks_ms()
            state = ARMED

    elif state == ARMED:
        if utime.ticks_diff(utime.ticks_ms(), last_tick) >= 1000:
            time_left -= 1
            display.show(str(time_left))
            last_tick = utime.ticks_ms()
        if time_left <= 0:
            speaker.on()
            state = EXPLOSION

    elif state == EXPLOSION:
        if pin_logo.is_touched():
            speaker.off()
            time_left = 20
            state = CONFIG
```
