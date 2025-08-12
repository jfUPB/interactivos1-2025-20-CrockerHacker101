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

# Activida 02: Bomba 2.0 :O  



