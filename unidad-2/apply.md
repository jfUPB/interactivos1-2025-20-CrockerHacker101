# Unidad 2


## 🛠 Fase: Apply  

# Actividad 5  
### Código  
```
from microbit import *
import utime

class Pixel:
    def __init__(self, pixelX, pixelY):
        self.pixelX = pixelX
        self.pixelY = pixelY

    def on(self):
        display.set_pixel(self.pixelX, self.pixelY, 9)

numbers_pixels = {
    3: [
        Pixel(1, 0), Pixel(2, 0), Pixel(3, 0),  
        Pixel(4, 1),
        Pixel(2, 2), Pixel(3, 2),                
        Pixel(4, 3),
        Pixel(1, 4), Pixel(2, 4), Pixel(3, 4)   
    ],
    2: [
        Pixel(1, 0), Pixel(2, 0), Pixel(3, 0),  
        Pixel(4, 1),
        Pixel(3, 2),
        Pixel(2, 3),
        Pixel(1, 4), Pixel(2, 4), Pixel(3, 4), Pixel(4, 4)
    ],
    1: [
        Pixel(2, 0),
        Pixel(2, 1),
        Pixel(2, 2),
        Pixel(2, 3),
        Pixel(2, 4),
    ]
}

while True:
    for number in [3, 2, 1]:
        display.clear()  
        for px in numbers_pixels[number]:
            px.on()
        sleep(1000)
```
