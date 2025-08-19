# Unidad 3

## 🔎 Fase: Set + Seek

# Actividad 01  

### Semaforo  

```python
from microbit import *
import utime

class Semaforo:
    def __init__(self,tr,ta,tv,col):
            self.tr = tr
            self.ta = ta
            self.tv = tv
            self.col = col
            display.set_pixel(self.col,0,9)
            self.startTime = utime.ticks_ms()
            self.state = "REDNIGGA"
   
    def update(self):
        if self.state == "REDNIGGA":
            if utime.ticks_diff(utime.ticks_ms(),self. startTime) >= self.tr:
                    display.set_pixel(self.col, 0,9)
                    display.set_pixel(self.col,1,9)
                    self.startTime = utime.ticks_ms()
                    self.state = "YENIGGA"

        elif self.state == "YENIGGA":
           if utime.ticks_diff(utime.ticks_ms(),self. startTime) >= self.tr:
                    display.set_pixel(self.col,0,9)
                    display.set_pixel(self.col,2,9)
                    self.startTime = utime.ticks_ms()
                    self.state = "GREEENIGGA"
               
        elif self.state == "GREENIGGA":
           if utime.ticks_diff(utime.ticks_ms(),self. startTime) >= self.tr:
                    display.set_pixel(self.col, 2,9)
                    display.set_pixel(self.col,0,9)
                    self.startTime = utime.ticks_ms()
                    self.state = "REDNIGGA"
    
     
semaforo1 = Semaforo(5000,2000,3000,0)
semaforo2 = Semaforo(3000,1000,2000,2)
semaforo3 = Semaforo(4000,3000,2000,4)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
```

# Activida 05:  

Construye el modelo de la bomba 3.0. Como ya tienes el código puedes tener un modelo muy preciso.  

### Modelo de la Máquina de Estados – Bomba 3.0  

**Estados principales**  
- **CONFIG** = Configuración del temporizador.  
- **ARMED** = Cuenta regresiva y posibilidad de desactivación con clave.  
- **EXPLODED** = Bomba explotada, requiere reinicio.  

**Eventos que disparan cambios**  
- **A** = Botón A (o por serial)  
- **B** = Botón B  
- **S** = Shake  
- **T** = Touch logo  
- **Timer** = Un segundo transcurrido  
- **Clave completa** = Secuencia `A-B-A` ingresada correctamente o incorrecta

### Tabla de Valores:
  
<img width="754" height="639" alt="Captura de pantalla 2025-08-14 214455" src="https://github.com/user-attachments/assets/79e9adfe-e792-4268-b7a8-84b8a5612889" />



